<template>
    <component :is="props.href ? 'a' : 'button'"
               class="btn btn-primary btn-xl"
               :type="props.href ? undefined : (props.type || 'button')"
               :href="props.href"
               :download="props.href ? props.download : undefined"
               :class="props.class">
        <i class="me-2" :class="props.icon"/>
        <span v-html="props.label"/>
    </component>
</template>

<script setup>
const props = defineProps({
    class: String,
    label: String,
    type: String,
    icon: String,
    href: String,
    download: [String, Boolean],
})
</script>

<style lang="scss" scoped>
@import "/src/scss/_theming.scss";

.btn-xl {
    @include generate-dynamic-styles-with-hash((
        xxxl: (padding: 1.125rem 2.3rem, font-size: 1.05rem),
        xxl:  (padding: 1rem 2rem, font-size: 1rem),
        lg:   (padding: 1rem 1.5rem, font-size: 0.9rem)
    ));

    border-radius: 4rem;
    font-weight: 400;
    font-family: $headings-font-family;
    text-transform: uppercase;
}
</style>
