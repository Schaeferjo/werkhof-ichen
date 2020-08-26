<template>
  <v-card-text v-if="veranstaltung.weitereZeiten">
    <p>
      <strong>Weitere Zeiten</strong>
    </p>
    <p v-for="(zeit, id) in zeiten" :key="id">
      <strong> {{ zeit }} Uhr </strong>
    </p>
  </v-card-text>
</template>

<script>
import { format, parseISO } from 'date-fns'
import { de } from 'date-fns/locale'

export default {
  props: {
    veranstaltung: {
      type: Object,
      required: true,
    },
  },
  computed: {
    zeiten() {
      return this.veranstaltung.weitereZeiten.map((zeit) => {
        const [von, bis] = [parseISO(zeit.von), parseISO(zeit.bis)]
        const opts = { locale: de }
        const timePattern = 'kk:mm'
        const datePattern = 'd. MMMM yyyy'
        return `${format(von, datePattern, opts)} | ${format(
          von,
          timePattern,
          opts
        )} - ${format(bis, timePattern, opts)}`
      })
    },
  },
}
</script>
