<template>
	<div class="pane" :class="colors[color]">
		<h2><slot></slot></h2>
	</div>
</template>

<script>

if (document.querySelector('.sortable-ghost')) {
	document.querySelector('body').style.cursor = "grabbing !important";
}

export default {


	data(){
		return {
			colors:["red", "green", "blue"],
		};
	},
	props:['color'],
}


</script>

<style>
	.pane{
		display:flex;
		justify-content: center;
		align-items: center;
		width: 200px;
		height:200px;
		border:solid 2px whitesmoke;
		border-radius: 10px;
		background:whitesmoke;
		text-align: center;
		user-select: none;
		cursor:grab;
		color: black;
	}

	.sortable-ghost{
		cursor: grabbing;
		opacity:0;
	}
	.ghost{
		opacity:.1;
	}

	h2{
		display:block;
		padding:0;
		margin:0;
		text-align:center;
		font-size:3rem;
	}

	.red{
		background-color: salmon;
	}
	.blue{
		background-color: lightblue;
	}
	.green{
		background-color: palegreen;
	}

</style>
