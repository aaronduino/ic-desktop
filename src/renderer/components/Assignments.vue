<template>
  <div>
    <div class="card" v-for="(section, key) in course.sections" v-bind:key="key">
      <h4 class="card-header">{{ section.name }}
        <span class="badge badge-success grade-badge">{{ section.grade | formatAsPercentage }}</span>
      </h4>
      <div class="card-body">
        <table class="table table-striped">
          <thead>
            <tr>
              <th scope="col" class="assignment">Assignment</th>
              <th scope="col" class="weight">
                Weight
                <span class="badge badge-primary weight-badge" v-if="section.weight">weight of {{ section.weight }}</span>
              </th>
              <th scope="col" class="received">Received</th>
              <th scope="col" class="possible">Possible</th>
              <th scope="col" class="percent">Percentage</th>
            </tr>
          </thead>
          <tbody>
            <tr v-for="(assignment, key) in section.assignments" v-bind:key="key">
              <td class="assignment">{{ assignment.name }}</td>
              <td class="weight">{{ assignment.weight }}</td>
              <td class="received">{{ assignment.ptsReceived }}</td>
              <td class="possible">{{ assignment.ptsPossible }}</td>
              <td class="percent">{{ assignment.grade | formatAsPercentage }}</td>
            </tr>
            <tr class="table-warning totals-row">
              <td class="assignment">Totals</td>
              <td class="weight"></td>
              <td class="received">{{ section.ptsReceived }}</td>
              <td class="possible">{{ section.ptsPossible }}</td>
              <td class="percent">{{ section.grade | formatAsPercentage }}</td>
            </tr>
          </tbody>
        </table>
      </div>
    </div>
  </div>
</template>

<script>
  export default {
    name: 'Assignments',
    computed: {
      course () {
        return this.$store.state.Student.courses[this.$route.params.id]
      }
    }
  }
</script>

<style lang="sass" scoped>
.card-header, .card-body
  font-size: 0.8rem

.card-body
  padding: 0rem

.card
  margin-bottom: 10px

.received, .possible, .percent, .weight
  text-align: right

.assignment
  width: 55%

.weight
  width: 10%

.possible
  width: 10%

.received
  width: 10%

.percent
  width: 15%

.weight-badge
  position: absolute
  top: 1em
  transform: translateX(-100%);

.grade-badge
  position: absolute
  right: 2%

.totals-row > td
  font-weight: bold
</style>

