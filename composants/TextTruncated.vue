<template>
    <div class="text-truncate-wrapper mb-4">
        <!-- Contenu texte avec transition -->
        <div class="text-content" :class="{ 'expanded': isExpanded }" :style="{ '--max-lines': truncateLines }">
            <p ref="textElement">{{ text }}</p>
        </div>

        <!-- Bouton intelligent qui disparaît progressivement quand inutile -->
        <button v-if="showReadMore" @click="toggleReadMore" class="read-more-btn" :class="{ 'expanded': isExpanded }"
            aria-live="polite">
            <span class="btn-content text-primary">
                {{ isExpanded ? 'Voir moins' : 'Lire la suite' }}
                <svg class="chevron" width="14" height="20" viewBox="0 0 24 24" fill="none">
                    <path d="M6 9L12 15L18 9" stroke="currentColor" stroke-width="2" stroke-linecap="round" />
                </svg>
            </span>
        </button>
    </div>
</template>

<script setup>
import { ref, computed, onMounted } from 'vue'

const props = defineProps({
    text: {
        type: String,
        default: ''
    },
    truncateLines: {
        type: Number,
        default: 3
    },
    charLimit: {
        type: Number,
        default: null
    }
})

const isExpanded = ref(false)
const textElement = ref(null)
const needsTruncation = ref(false)

// Vérifie si le texte nécessite une troncature
onMounted(() => {
    if (textElement.value) {
        const lineHeight = parseInt(getComputedStyle(textElement.value).lineHeight)
        const elementHeight = textElement.value.clientHeight
        const maxHeight = lineHeight * props.truncateLines

        needsTruncation.value = elementHeight > maxHeight
    }
})

const showReadMore = computed(() => {
    return props.text?.trim() && (needsTruncation.value || (props.charLimit && props.text.length > props.charLimit))
})

function toggleReadMore() {
    isExpanded.value = !isExpanded.value
}
</script>

<style scoped>
.text-truncate-wrapper {
    --line-height: 1.5em;
    --transition-duration: 0.4s;
    --easing: cubic-bezier(0.25, 0.1, 0.25, 1);
    --text-color: #333;
    --link-color: #4f46e5;
    --link-hover: #3730a3;
}

.text-content {
    position: relative;
    overflow: hidden;
    transition: max-height var(--transition-duration) var(--easing);
    max-height: calc(var(--line-height) * var(--max-lines));
}

.text-content.expanded {
    max-height: none !important;
}

.text-content::after {
    content: '';
    position: absolute;
    bottom: 0;
    left: 0;
    right: 0;
    height: calc(var(--line-height) * 1.5);
    background: linear-gradient(to bottom, rgba(255, 255, 255, 0) 0%, rgba(255, 255, 255, 0.9) 80%);
    opacity: 1;
    transition: opacity var(--transition-duration) var(--easing);
}

.text-content.expanded::after {
    opacity: 0;
}

.read-more-btn {
    display: inline-flex;
    align-items: center;
    background: none;
    border: none;
    color: var(--link-color);
    cursor: pointer;
    padding: 0.25em 0;
    font-size: 0.95em;
    font-weight: 500;
    transition: all 0.2s ease;
    margin-top: 0.5em;
}

.read-more-btn:hover {
    color: var(--link-hover);
}

.btn-content {
    display: inline-flex;
    align-items: center;
    gap: 0.3em;
}

.chevron {
    transition: transform var(--transition-duration) var(--easing);
}

.read-more-btn.expanded .chevron {
    transform: rotate(180deg);
}

/* Animation douce du texte */
p {
    margin: 0;
    line-height: var(--line-height);
    color: var(--text-color);
    animation: fadeIn var(--transition-duration) var(--easing);
}

@keyframes fadeIn {
    from {
        opacity: 0.6;
        transform: translateY(2px);
    }

    to {
        opacity: 1;
        transform: translateY(0);
    }
}
</style>