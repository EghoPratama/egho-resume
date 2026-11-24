<template>
    <Article class="article-profile"
             :model="model">
        <h1 class="title display-1 mb-3"
            v-html="title"/>

        <InlineLinkList :items="InlineLinkListLinks"/>

        <div class="items-wrapper py-2 py-lg-3">
            <ArticleProfileItem v-for="item in model.items"
                                :item="item"/>
        </div>

        <div v-if="resumeUrl"
             class="resume-download pb-2 pb-lg-3">
            <XLButton :href="resumeUrl"
                      :download="resumeFileName"
                      icon="fa-solid fa-download"
                      :label="localizeFromStrings('download_resume')"/>
        </div>

        <SocialLinks :items="socialLinks"
                     class="pt-lg-1"
                     size="3"
                     variant="dark"/>
    </Article>
</template>

<script setup>
import {computed, inject} from "vue"
import Article from "/src/vue/components/articles/base/Article.vue"
import ArticleProfileItem from "/src/vue/components/articles/profile/ArticleProfileItem.vue"
import SocialLinks from "/src/vue/components/widgets/SocialLinks.vue"
import InlineLinkList from "/src/vue/components/widgets/InlineLinkList.vue"
import XLButton from "/src/vue/components/widgets/XLButton.vue"
import {useUtils} from "/src/composables/utils.js"

const utils = useUtils()

const props = defineProps({
    model: {
        /** @type {Article} **/
        type: Object,
        required: true
    }
})

/** @type {Function} */
const localize = inject("localize")

/** @type {Function} */
const localizeFromStrings = inject("localizeFromStrings")

const resumeUrl = computed(() => {
    const path = props.model.getSetting("resume_pdf_url", null)
    return path ? utils.resolvePath(path) : null
})

const resumeFileName = computed(() => {
    return resumeUrl.value ? resumeUrl.value.split("/").pop() : null
})

/** @type {{value:Profile}} */
const profile = inject("profile")

/** @type {{value:Boolean}} */
const isScreenXlOrLarger = inject("isScreenXlOrLarger")

const title = computed(() => {
    return localize(
        props.model.section.locales,
        isScreenXlOrLarger.value ? "title" : "title_short"
    )
})

const InlineLinkListLinks = computed(() => {
    const contactIds = props.model.getSetting("contact_list_ids", [])
    return contactIds.map(contactId => {
        return profile.value.getContactOptionWithId(contactId)
    }).filter(contact => Boolean(contact))
})

const socialLinks = computed(() => {
    const contactIds = props.model.getSetting("contact_circles_ids", [])
    return contactIds.map(contactId => {
        return profile.value.getContactOptionWithId(contactId)
    }).filter(contact => Boolean(contact))
})
</script>

<style lang="scss" scoped>
@import "/src/scss/_theming.scss";

h1.title {
    font-weight: bold;
    text-transform: uppercase;
    letter-spacing: 3px;
    @include media-breakpoint-down($navigation-sidebar-breakpoint) {
        display: none;
    }
}
</style>