<template>
  <nav
    id="side-nav"
    class="side-nav"
  >
    <div
      v-for="group in groupedList"
      :key="group.id"
      class="side-nav__group"
    >
      <div class="side-nav__group-label">
        {{ group.id }}
      </div>
      <ul class="side-nav__list">
        <li
          v-for="item in group.components"
          :key="item.name.toLowerCase()"
          class="side-nav__item"
        >
          <router-link
            class="side-nav__link"
            active-class="side-nav__link--active"
            :to="item.path"
          >
            {{ item.name }}
          </router-link>
        </li>
      </ul>
    </div>
  </nav>
</template>

<script>
export default {
  name: 'SideNav',
  props: {
    list: {
      type: Array,
      required: true,
    },
  },
  computed: {
    groupedList() {
      return this.list.reduce((acc, cur) => {
        if (acc.map[cur.group] === undefined) {
          acc.map[cur.group] = {
            id: cur.group,
            components: [],
          };
          acc.set.push(acc.map[cur.group]);
        }
        acc.map[cur.group].components.push(cur);
        return acc;
      }, {
        set: [],
        map: {},
      }).set;
    },
  },
};
</script>

<style lang="scss">
.side-nav{
  $side-nav-line-height: 40px;

  flex-shrink: 0;
  width: 240px;
  height: 100%;

  border-right: solid 1px $color-dark-10;

  &__group{
    margin: 0 20px;

    &-label{
      border-bottom: solid 1px $color-dark-10;
      margin: 0;

      color: $color-dark-60;
      font-size: 14px;
      line-height: $side-nav-line-height;
      font-weight: normal;
      text-transform: uppercase;
    }
  }
  &__list{
    list-style: none;
    padding: 0;
    margin: 10px 0 20px;
    line-height: $side-nav-line-height;
  }
  &__link{
    display: block;

    color: $color-dark-80;
    text-decoration: none;

    &:hover{
      color: $color-major;
    }
    &--active{
      background: rgba($color-major, .32);
    }
  }

}
</style>
