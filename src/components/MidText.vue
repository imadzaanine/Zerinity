<template>
    <div class="MidTextArea">
        <div class="Midtext">
            <h1>Hi <br> Can I help you with anything today ?</h1>
        </div>
    </div>
</template>

<script>
export default {
    name: 'MidText',
};
</script>

<style scoped>
.MidTextArea {
    display: flex;
    justify-content: center;
    align-items: center;
}
.Midtext{
    display: flex;
    padding: 30px 10px;
    flex-direction: column;
    align-items: center;
    gap: 13px;
    border-radius: 30px;
    background: rgba(206, 229, 255, 0.32);
    text-align: center;
}
h1{
    color: #CEE5FF;
    text-align: center;
    font-family: "Inter" , sans-serif;
    font-size: 32px;
    font-style: normal;
    font-weight: 700;
    line-height: normal;
}
</style>