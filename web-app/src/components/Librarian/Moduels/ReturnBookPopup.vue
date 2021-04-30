<template>
    <div id="popup">
        <div id="popup-inner">
            <h1>
                Return Book
            </h1>
        </div>
    </div>    
</template>

<script>
export default {
    setup() {
        
    },
}
</script>

<style scoped>
#popup {
    position: fixed;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
    z-index: 99;
    background-color: rgba(0, 0, 0, 0.2);

    display: flex;
    align-items: center;
    justify-content: center;
}

#popup-inner {
    background: #FFF;
    padding: 32px;
}


</style>