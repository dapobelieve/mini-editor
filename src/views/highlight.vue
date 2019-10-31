<template>
	<div class="texts">
		<div>
			<div onmousedown="event.preventDefault()" class="menu z-20" v-show="showLink"  :style="{left: `${x}px`, top: `${y}px`} ">
				<span>
					<input id="search" class="link"  placeholder="Enter a link" type="text">
					<a class="close-link" @click.prevent="toggleLinkMenu" href>X</a>
				</span>
			</div>
			<div onmousedown="event.preventDefault()" class="menu" v-show="showMenu" :style="{left: `${x}px`, top: `${y}px`}">
				<div class="item-icons">
					<span @click="handleCommand('bold')">
						<i class="fa fa-bold item-icon-double"></i>						
					</span>
					<span @click="handleCommand('italic')">
						<i class="fa fa-italic"></i>
					</span>
				</div>
				<div class="item-icons">
					<span @click="handleCommand('h3')">
						<i class="fa fa-heading item-icon-double"></i>
					</span>
					<span @click="handleCommand('h4')">
						<small><i class="fa fa-heading"></i></small>
					</span>
				</div>
				<div class="item-icons">
					<span @click="handleCommand('quote')">
						<i class="fa fa-quote-right"></i>
 					</span>
				</div>
				<div class="item-icons">
					<span @click="handleCommand('ul')">
						<i class="fa fa-list-ul item-icon-double"></i>
					</span>
					<span @click="handleCommand('ol')">						
						<i class="fa fa-list-ol"></i>
					</span>
				</div>
				<div class="item-icons">
					<span @click.prevent="showLink = true;">
						<i class="fa fa-link"></i>
					</span>
				</div>
			</div>
			<div id="editor" v-html="text" contenteditable="true">
			</div>
		</div>
	</div>
</template>

<script>
export default {
	data () {
		return {
			selection: {},
			x: 0,
			y: 0,
			showMenu: false,
			showLink: false,
			text: `<section>
				<p>My father’s family name being Pirrip, and my Christian name Philip, my infant tongue could make of both names nothing longer or more explicit than Pip. So, I called myself Pip, and came to be called Pip.</p>

				<p>I give Pirrip as my father’s family name, on the authority of his tombstone and my sister,—Mrs. Joe Gargery, who married the blacksmith. As I never saw my father or my mother, and never saw any likeness of either of them (for their days were long before the days of photographs), my first fancies regarding what they were like were unreasonably derived from their tombstones. The shape of the letters on my father’s, gave me an odd idea that he was a square, stout, dark man, with curly black hair. From the character and turn of the inscription, 
				“Also Georgiana Wife of the Above,” I drew a childish conclusion that my mother was freckled and sickly. To five little stone lozenges, each about a foot and a half long, which were arranged in a neat row beside their grave, and were sacred to the memory of five little brothers of mine,—who gave up trying to get a living, exceedingly early in that universal struggle,—I am indebted for a belief 
				I religiously entertained that they had all been born on their backs with their hands in their trousers-pockets, and had never taken them out in this state of existence.</p>

				<h3>Ours was the marsh country, down by the river, within, as the river wound, twenty miles of the sea. My first most vivid and broad impression of the identity of things seems to me to have been gained on a memorable raw afternoon towards evening.
				</h3>
				<p> At such a time I found out for certain that this bleak place overgrown with nettles was the churchyard; and that Philip Pirrip, late of this parish, and also Georgiana wife of the above, were dead and buried; and that Alexander, Bartholomew, Abraham, Tobias, and Roger, infant children of the aforesaid, were also dead and buried; and that the dark flat wilderness beyond the churchyard, intersected with dikes and mounds and gates, with scattered cattle feeding on it, was the marshes; and that the low leaden line beyond was the river; and that the distant savage lair from which the wind was rushing was the sea; and that the small bundle of shivers growing afraid of it all and beginning to cry, was Pip.</p>
				</section>`
			}
	},
	created() {
		document.addEventListener('selectionchange', this.selected);			
	},
	methods: {
		toggleLinkMenu (event)
		{
			console.log(event);
			// this.showLink = !this.showLink;
		},
		handleCommand(command) {
			// array of tags that could surround a text block
			let blockTags = ['h3', 'p', 'h4', 'blockquote'];

			let sel = document.getSelection();

			let selectRange = sel.getRangeAt(0);
			let currentParent = selectRange.commonAncestorContainer.parentNode;
			let content = selectRange.commonAncestorContainer.data.toString();
			let currentTagName = currentParent.nodeName.toLowerCase();
			let parent, tagName, newTag;

			console.log(currentTagName);
			console.log('content::before')
			console.log(content)

			switch (command) {
				case "bold":
				document.execCommand('bold', false, null);
				break;
				case "italic":
					document.execCommand('italic', false, null);
				break;
				case "h3":
					
					parent = blockTags.includes(currentTagName, 0) == true ? currentParent : currentParent.parentNode;

					if (!blockTags.includes(currentTagName))
						content = selectRange.commonAncestorContainer.parentElement.parentElement.innerHTML;
					
					
					currentTagName = parent.nodeName.toLowerCase();

					console.log('content::after')
					console.log(content)
					
					tagName = currentTagName !== 'h3' ? 'h3' : 'p';

					newTag = document.createElement(tagName);
					newTag.innerHTML = content;

					parent.parentNode.replaceChild(newTag, parent);

					this.showMenu = false;
				break;
				case "h4":

					parent = blockTags.includes(currentTagName, 0) == true ? currentParent : currentParent.parentNode;

					if (!blockTags.includes(currentTagName))
						content = selectRange.commonAncestorContainer.parentElement.parentElement.innerHTML;
					
					
					currentTagName = parent.nodeName.toLowerCase();

					console.log(content)
					
					tagName = currentTagName !== 'h4' ? 'h4' : 'p';

					newTag = document.createElement(tagName);
					newTag.innerHTML = content;

					parent.parentNode.replaceChild(newTag, parent);

					this.showMenu = false;
				break;
				case "ul":
					document.execCommand('insertUnorderedList', false);
				break;
				case "ol":
					document.execCommand('insertorderedlist', false);
				break;
				case "quote":
					parent = blockTags.includes(currentTagName, 0) == true ? currentParent : currentParent.parentNode;

					if (!blockTags.includes(currentTagName))
						content = selectRange.commonAncestorContainer.parentElement.parentElement.innerHTML;
					
					
					currentTagName = parent.nodeName.toLowerCase();

					console.log('content::after')
					console.log(content)
					
					tagName = currentTagName !== 'blockquote' ? 'blockquote' : 'p';

					newTag = document.createElement(tagName);
					newTag.innerHTML = content;

					parent.parentNode.replaceChild(newTag, parent);

					this.showMenu = false;
				break;
			}
		},
		selected () {
			this.showLink = false;
      		this.selection = window.getSelection();
	    	const { x, y, width} = this.selection.getRangeAt(0).getBoundingClientRect();

	    	if (width > 0) {
	      	this.x = x + (width / 2);
	      	this.y = y + window.scrollY - 20;
	      	this.showMenu = true;
	      	return;
	    	}

	    	this.showMenu = false;
    }
   
	}
}
</script>

<style scoped>


::selection {
	background: #252525;
	color: #FFFFFF;
}

.z-20 {
	z-index: 20;
}
.menu {  
	height: 41px;
	width: 277px;
	padding: 5px 15px;
	background: #252525 0% 0% no-repeat padding-box;
	box-shadow: 0px 3px 6px #00000033;
	border: 1px solid #0000001A;
	opacity: 1;
	border-radius: 5px;  
	position: absolute; 
	top: 0;  left: 0;  
	transform: translate(-50%, -100%);
	transition: 0.5s all;  
	display: flex;  
	justify-content: space-between;  
	align-items: center;
}

.link {
	border: 0;
	/*height: 24px;*/
	width: 269px;
	margin-right: 10px;
	background: transparent;
	color: #fff;
	letter-spacing: 0;
	padding: 5px 5px;
	border-color: transparent;
}

.link::-webkit-input-placeholder {
	color: #565656;
}

.link:focus {
	border: 0;
}
.close-link {
	text-decoration: none; 
	color: #fff; 
	font-size: 13px; 
	opacity: 0.45; 
	position: absolute;
	margin-left: -22px;
	margin-top: 3px;
}

.item-icons {  
	color: #FFF;  
	padding-right: 15px;
	border-right: 1px solid #544949;
	border-right-width: thin;
}

.item-icons span:hover {
	cursor: pointer;
	color: #ff3;
}

.item-icons:last-child { 
	padding-right: 0;
	border-right: none;
}

.item-icon-double {
	margin-right: 10px;
}

blockquote {
    margin: 0;
}

blockquote p {
    padding: 15px;
    background: #eee;
    border-radius: 5px;
}

blockquote p::before {
    content: '\201C';
}

blockquote p::after {
    content: '\201D';
}



</style>