<template>
  <v-footer
    id="dashboard-core-footer"
  >
    <v-container>
      <v-row
        align="center"
        no-gutters
      >

        <v-spacer class="hidden-sm-and-down" />

        <v-col
          cols="12"
          md="auto"
        >
          <div class="body-1 font-weight-light pt-6 pt-md-0 text-center">
            &copy; 2021, made with
            <v-icon size="18">
              mdi-heart
            </v-icon>
            by CuongNM48</a> for a better web.
          </div>
        </v-col>
      </v-row>
    </v-container>
  </v-footer>
</template>

<script>
  export default {
    name: 'DashboardCoreFooter',

    data: () => ({
      links: [
        {
          href: '#',
          text: 'Creative Tim'
        },
        {
          href: '#',
          text: 'About Us'
        },
        {
          href: '#',
          text: 'Blog'
        },
        {
          href: '#',
          text: 'Licenses'
        }
      ]
    })
  }
</script>

<style lang="sass">
  #dashboard-core-footer
    a
      color: #3c4858
      font-size: .825rem
      font-weight: 500
      text-decoration: none
      text-transform: uppercase
</style>
