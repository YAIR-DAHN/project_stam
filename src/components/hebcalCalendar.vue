<template>
    <div>
      <div id="calendar"></div>
      <FullCalendar />
    </div>
  </template>
  
  <script>
  import FullCalendar from '@fullcalendar/vue';
  import dayGridPlugin from '@fullcalendar/daygrid';
  
  export default {
    components: {
      FullCalendar,
    },
    data() {
      return {
        calendarOptions: {
          plugins: [dayGridPlugin],
          headerToolbar: {
            left: 'title',
            right: 'prev,next today',
          },
          events: {
            // add &c=on&geonameid=[locationID] for candle-lighting times
            url:
              'https://www.hebcal.com/hebcal?cfg=fc&v=1&i=off&maj=on&min=on&nx=on&mf=on&ss=on&mod=on&lg=s&s=on',
            cache: true,
          },
        },
      };
    },
    mounted() {
      // optional: bind keyboard left/right arrow keys
      // to move calendar forward/backward by a month
      document.addEventListener('keydown', (e) => {
        if (e.key === 'ArrowLeft' && !e.metaKey) {
          this.$refs.calendar.getApi().prev();
        } else if (e.key === 'ArrowRight' && !e.metaKey) {
          this.$refs.calendar.getApi().next();
        }
      });
    },
  };
  </script>
  
  <style>
  @import '~@fullcalendar/common/main.css';
  @import '~@fullcalendar/daygrid/main.css';
  </style>
  