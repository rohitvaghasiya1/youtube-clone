<template>
  <q-layout view="hHh lpR fFf">
    <q-header class="bg-white text-grey-8 q-py-xs" height-hint="58">
      <q-toolbar>
        <q-btn
          flat
          dense
          round
          @click="miniState = !miniState"
          aria-label="Menu"
          icon="menu"
        />

        <q-btn flat no-caps no-wrap class="q-ml-xs">
          <q-icon :name="fabYoutube" color="red" size="28px" />
          <q-toolbar-title shrink class="text-weight-bold">
            YouTube
          </q-toolbar-title>
        </q-btn>

        <q-space />

        <div
          v-if="$q.screen.gt.sm"
          class="YL__toolbar-input-container header-search-bar row no-wrap"
        >
          <div class="col">
            <q-input
              rounded
              outlined
              v-model="search"
              placeholder="Search"
              @focus="showSearchIcon = true"
              @blur="showSearchIcon = false"
              class="col"
            >
              <template v-if="showSearchIcon" v-slot:prepend>
                <q-icon name="search" />
              </template>
              <template v-slot:append>
                <q-icon name="keyboard" class="q-mr-md" />
                <q-btn flat color="grey-3" text-color="grey-8" icon="search" />
              </template>
            </q-input>
          </div>
          <div class="col-1 text-right">
            <q-btn flat round color="grey-3" icon="mic" text-color="grey-8" />
          </div>
        </div>

        <q-space />

        <div class="q-gutter-sm row items-center no-wrap">
          <q-btn round flat icon="more_vert">
            <q-menu auto-close :offset="[110, 0]">
              <q-list style="min-width: 150px">
                <q-item clickable>
                  <q-item-section>Contact data</q-item-section>
                </q-item>
                <q-item clickable>
                  <q-item-section>Block</q-item-section>
                </q-item>
                <q-item clickable>
                  <q-item-section>Select messages</q-item-section>
                </q-item>
                <q-item clickable>
                  <q-item-section>Silence</q-item-section>
                </q-item>
                <q-item clickable>
                  <q-item-section>Clear messages</q-item-section>
                </q-item>
                <q-item clickable>
                  <q-item-section>Erase messages</q-item-section>
                </q-item>
              </q-list>
            </q-menu>
          </q-btn>
          <q-btn
            :outline="$q.screen.gt.sm"
            :flat="$q.screen.lt.md"
            :class="$q.screen.lt.md ? 'q-pa-none' : ''"
            rounded
            :color="$q.screen.gt.sm ? 'primary' : 'grey-8'"
            icon="account_circle"
          >
            <span v-if="$q.screen.gt.sm" class="q-ml-sm">Sign In</span>
          </q-btn>
          <q-btn round dense flat color="grey-8" icon="invert_colors">
            <q-tooltip>Change mode</q-tooltip>
          </q-btn>
        </div>
      </q-toolbar>
    </q-header>

    <q-drawer
      v-model="drawer"
      show-if-above
      :mini="!drawer || miniState"
      @click.capture="drawerClick"
      :width="240"
      :breakpoint="767"
    >
      <q-scroll-area class="fit" :horizontal-thumb-style="{ opacity: 0 }">
        <q-list padding>
          <q-item v-for="link in links1" :key="link.text" v-ripple clickable>
            <q-item-section avatar>
              <q-icon color="grey-8" :name="link.icon" />
            </q-item-section>
            <q-item-section>
              {{ link.text }}
            </q-item-section>
          </q-item>

          <q-separator class="q-my-md" />

          <q-item v-for="link in links2" :key="link.text" v-ripple clickable>
            <q-item-section avatar>
              <q-icon color="grey-8" :name="link.icon" />
            </q-item-section>
            <q-item-section>
              {{ link.text }}
            </q-item-section>
          </q-item>

          <q-separator class="q-mt-md q-mb-lg" />

          <div class="q-px-md text-grey-9" v-if="!miniState">
            <div class="row items-center q-gutter-x-sm q-gutter-y-xs">
              <a
                v-for="button in buttons1"
                :key="button.text"
                class="YL__drawer-footer-link"
                href="javascript:void(0)"
              >
                {{ button.text }}
              </a>
            </div>
          </div>
          <div class="q-py-md q-px-md text-grey-9" v-if="!miniState">
            <div class="row items-center q-gutter-x-sm q-gutter-y-xs">
              <a
                v-for="button in buttons2"
                :key="button.text"
                class="YL__drawer-footer-link"
                href="javascript:void(0)"
              >
                {{ button.text }}
              </a>
            </div>
          </div>
        </q-list>
      </q-scroll-area>
    </q-drawer>

    <q-page-container>
      <router-view />
    </q-page-container>
  </q-layout>
</template>

<script>
import { ref } from "vue";
import { fabYoutube } from "@quasar/extras/fontawesome-v6";

export default {
  name: "MainLayout",

  setup() {
    const search = ref("");
    const showSearchIcon = ref(false);

    const miniState = ref(false);

    return {
      drawer: ref(false),
      miniState,

      drawerClick(e) {
        // if in "mini" state and user
        // click on drawer, we switch it to "normal" mode
        if (miniState.value) {
          miniState.value = false;

          // notice we have registered an event with capture flag;
          // we need to stop further propagation as this click is
          // intended for switching drawer to "normal" mode only
          e.stopPropagation();
        }
      },
      fabYoutube,
      search,
      showSearchIcon,

      links1: [
        { icon: "home", text: "Home" },
        { icon: "music_video", text: "Shorts" },
        { icon: "ondemand_video", text: "Subscriptions" },
        { icon: "video_library", text: "Library" },
        { icon: "history", text: "History" },
      ],
      links2: [
        { icon: "settings", text: "Settings" },
        { icon: "flag", text: "Report history" },
        { icon: "help", text: "Help" },
        { icon: "feedback", text: "Send feedback" },
      ],
      buttons1: [
        { text: "About" },
        { text: "Press" },
        { text: "Copyright" },
        { text: "Contact us" },
        { text: "Creators" },
        { text: "Advertise" },
        { text: "Developers" },
      ],
      buttons2: [
        { text: "Terms" },
        { text: "Privacy" },
        { text: "Policy & Safety" },
        { text: "Test new features" },
      ],
    };
  },
};
</script>

<style lang="sass">
.YL

  &__toolbar-input-container
    min-width: 100px
    width: 55%

  &__toolbar-input-btn
    border-radius: 0
    border-style: solid
    border-width: 1px 1px 1px 0
    border-color: rgba(0,0,0,.24)
    max-width: 60px
    width: 100%

  &__drawer-footer-link
    color: inherit
    text-decoration: none
    font-weight: 500
    font-size: .75rem

    &:hover
      color: #000
</style>

<style lang="scss">
.header-search-bar {
  max-width: 732px;
  margin: auto;
  width: 100%;
  @media screen and (max-width: 1439px) {
    max-width: 600px;
  }
  .q-field__control {
    height: 40px;
    padding-right: 0;
    .q-field__native {
      padding: 0;
    }
    .q-field__marginal {
      height: 40px;
      .q-btn-item {
        border-left: 1px solid rgba(0, 0, 0, 0.24);
        width: 68px;
        border-radius: 0 50px 50px 0;
        height: 40px;
      }
    }
  }
}
</style>
