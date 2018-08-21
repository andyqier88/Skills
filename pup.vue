
<template>
  <div>
	<div class="mask">
	  <div class="content-wrapper">
		<div class="content">
		  <span >
		    <slot name="content"></slot>
		  </span>
	  	</div>
	    <div class="bottom-btn">
		  <slot name="left-btn"></slot>
		  <slot name="right-btn"></slot>
	  	</div>
	  </div>
    </div>
  </div>
</template>

<style lang="less" scoped>
/* eslint-disable */
.mask {
  position: fixed;
  left: 0;
  right: 0;
  top: 0;
  bottom: 0;
  background: rgba(0, 0, 0, 0.55);
}
.content-wrapper {
  background: #fff;
  width: 80%;
  margin: 0 auto;
  margin-top: 55%;
  padding-bottom: 15px;
  border-radius: 5px;
  text-align: center;
}
.content {
  padding: 35px;
}
.bottom-btn {
  display: flex;
  color: #fff;
  padding: 0 15px;
  font-size: 16px;
}
</style>
