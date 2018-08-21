
<template>
    <div>
        <div>
            <div class="list">
                <ul >
                    <slot></slot>
                </ul>
            </div>
        </div>
    </div>
</template>

<style lang="less" scoped>
/* eslint-disable */
    .list ul{
        display: flex;
        justify-content: space-between;
        flex-wrap: wrap;
    }
</style>
