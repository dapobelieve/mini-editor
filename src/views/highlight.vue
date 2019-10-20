<template>
	<div class="texts">
		<div>
			<div class="menu" :style="{left: `${x}px`, top: `${y}px`}">
				<input class="link" placeholder="Enter link" type="text">
				<a @click.prevent="" href="">X</a>
			</div>
			<!-- <div class="menu" v-show="showMenu" :style="{left: `${x}px`, top: `${y}px`}">
				<span class="item-icons">
					<i class="fa fa-bold item-icon-double"></i>
					<i class="fa fa-italic"></i>
				</span>
				<span class="item-icons">
					<i class="fa fa-heading item-icon-double"></i>
					<small><i class="fa fa-heading"></i></small>
				</span>
				<span class="item-icons">
					<i class="fa fa-quote-right"></i>
				</span>
				<span class="item-icons">
					<i class="fa fa-list-ul item-icon-double"></i>
					<i class="fa fa-list-ol"></i>
				</span>
				<span class="item-icons"><i class="fa fa-link"></i></span>
			</div> -->
			<div contenteditable="true">
				Lorem ipsum dolor sit amet, consectetur adipisicing elit. Quod temporibus tenetur cumque culpa odio laudantium doloremque! Perspiciatis dolore nesciunt cupiditate ullam ducimus et cum, nisi voluptas veritatis obcaecati debitis, explicabo provident, eum iste eius. Quisquam sapiente, amet, expedita facere, vitae voluptatibus recusandae a ex voluptate accusantium molestiae! Voluptatibus, nobis, eos! Quae, asperiores! Similique ullam blanditiis qui ut voluptates doloremque, quo nemo reiciendis incidunt, repellendus, fugit id distinctio delectus nisi dolorum neque! Est quibusdam distinctio optio dicta ipsam consequatur ratione delectus sit vel quis unde impedit minus modi omnis iure ad voluptates, molestiae! Maxime ipsa deserunt fugiat qui veritatis aliquid temporibus at, nostrum itaque architecto unde explicabo similique doloribus vel sed amet vitae saepe odio nam aspernatur reprehenderit rerum ab. Fugiat quisquam soluta enim, explicabo maiores quaerat impedit provident rerum, fuga assumenda ipsam accusantium fugit possimus? Molestiae blanditiis laborum quasi amet tempora praesentium fuga sequi. Quo vero praesentium placeat, nobis perferendis iusto suscipit nihil fugit possimus obcaecati, alias corporis consectetur accusantium veniam iste quisquam fuga voluptatum culpa voluptates adipisci nemo, tempore quae. Excepturi exercitationem modi laboriosam minus quos temporibus! Cupiditate, quisquam odit labore consectetur sit, accusantium deleniti tempora nisi optio, magnam, natus! Facilis labore amet, explicabo temporibus quia possimus nemo! Sint.
			</div>
		</div>
	</div>
</template>

<script>
export default {
	data () {
		return {
			x: 0,
			y: 0,
			showMenu: false,
		}
	},
	computed: {
		
	},
	created() {
		window.addEventListener('mouseup', this.onMouseup)
	},
	methods: {
		onMouseup () {
			this.showMenu = false;
      const selection = window.getSelection();
      // if (selection.toString() !== "")
      	const { x, y, width} = selection.getRangeAt(0).getBoundingClientRect();
      	console.log(width);

      	if (width > 0) {
	      	this.x = x + (width / 2);
	      	this.y = y + window.scrollY - 20;
	      	this.showMenu = true;
	      	return;
      	}else {
      		this.showMenu = false;
      	}      	
    }
	}
}
</script>

<style scoped>
::selection {
	background: #252525;
	color: #FFFFFF;
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
	transition: 0.2s all;  
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
}

.link::-webkit-input-placeholder {
	color: #fff;
}

.link:focus {
	border: 0;
}

.item-icons {  
	color: #FFF;  
	cursor: pointer;
	padding-right: 15px;
	border-right: 1px solid #544949;
	border-right-width: thin;
}

.item-icons:last-child { 
	padding-right: 0;
	border-right: none;
}

.item-icon-double {
	margin-right: 10px;
}

</style>