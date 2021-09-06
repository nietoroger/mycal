<template>
  <div class="hello">
    <label for>Calendario</label>
    <Fullcalendar :options="options" />
  </div>
</template>

<script>
import { getUsers } from "@/services/data.service";
import Fullcalendar from "@fullcalendar/vue";
import dayGridPlugin from "@fullcalendar/daygrid";
import timeGridPlugin from "@fullcalendar/timegrid";
import interactionPlugin from "@fullcalendar/interaction";
import listPlugin from "@fullcalendar/list";
import resourceTimelinePlugin from "@fullcalendar/resource-timeline";
export default {
  async mounted() {
    const data = await getUsers().then((r) => {
      return r.json();
    });

    this.resources = data.map((x) => {
      return {
        id: x.id,
        title: x.name,
      };
    });
  },
  components: {
    Fullcalendar,
  },
  data() {
    return {
      options: {
        resources: [],
        plugins: [
          dayGridPlugin,
          timeGridPlugin,
          interactionPlugin,
          listPlugin,
          resourceTimelinePlugin,
        ],
        initialView: "resourceTimeline",
        resources: this.resources,
      },
    };
  },
};
</script>

</style>
