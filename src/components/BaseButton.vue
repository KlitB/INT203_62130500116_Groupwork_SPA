<template>
    <div>
        <button :class="[buttonbg]" class="btn p-2 text-white font-bold">{{buttontext}} ❤️</button>
    </div>
</template>

<script>
export default {
    props : [
        "buttonbg",
        "buttontext"
    ]
}
</script>