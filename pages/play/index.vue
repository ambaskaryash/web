<script setup lang="ts">
import MyUpcomingMatches from "~/components/MyUpcomingMatches.vue";
import Matchmaking from "~/components/matchmaking/Matchmaking.vue";
import OpenMatches from "~/components/match/OpenMatches.vue";
import CustomMatch from "~/components/CustomMatch.vue";
</script>

<template>
  <div class="flex flex-col gap-4">
    <template v-if="matchmakingAllowed">
      <Matchmaking></Matchmaking>
      <Separator class="my-4" />
    </template>
    <template v-else-if="canCreateMatch">
      <CustomMatch class="bg-card p-8 rounded-lg" />
    </template>

    <MyUpcomingMatches>
      <Separator class="my-4" />
    </MyUpcomingMatches>

    <Card class="p-4">
      <CardHeader>
        <CardTitle>{{ $t("pages.play.open_matches.title") }}</CardTitle>
        <CardDescription>
          {{ $t("pages.play.open_matches.description") }}
        </CardDescription>
      </CardHeader>
      <OpenMatches> </OpenMatches>
    </Card>

    <div id="pagination"></div>
  </div>
</template>

<script lang="ts">
import { useApplicationSettingsStore } from "~/stores/ApplicationSettings";

export default {
  data() {
    return {
      page: 1,
      perPage: 10,
    };
  },
  computed: {
    me() {
      return useAuthStore().me;
    },
    regions() {
      return useApplicationSettingsStore().availableRegions;
    },
    matchmakingAllowed() {
      return useApplicationSettingsStore().matchmakingAllowed;
    },
    canCreateMatch() {
      return useApplicationSettingsStore().canCreateMatch;
    },
  },
};
</script>
