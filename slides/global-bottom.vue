<template>
    <footer v-if="$slidev.nav.currentLayout !== 'cover'" class="absolute bottom-0 left-0 right-0 p-2">
      <div v-if="$slidev.nav.currentLayout == 'image-right'" class="text-small text-light">
        {{ $slidev.nav.currentPage }}
      </div>
      <div v-else class="float-right text-small text-light">
        {{ $slidev.nav.currentPage }}
      </div>
    </footer>
</template>