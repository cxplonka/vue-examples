<template>
  <div>
    <q-search v-model="search" clearable="true"/>
    <q-tree
      v-bind:nodes="tickable"
      color="primary"
      default-expand-all
      v-bind:ticked.sync="ticked"
      v-bind:tick-strategy="tickStrategy"
      v-bind:filter="tickFilter"
      node-key="label"
    >

    <div slot="body-badges" slot-scope="prop" class="row items-center">
      <q-checkbox>{{ prop.node.label }}</q-checkbox>
      <q-icon :name="prop.node.icon || 'star'" color="orange" size="28px" class="q-mr-sm" />
      <div class="text-weight-bold text-primary">{{ prop.node.label }}</div>
      <q-chip floating color="primary">22</q-chip>
    </div>

  </q-tree>
  </div>
</template>

<script>
export default {
  data: () => ({
    search: '',
    ticked: [],
    tickStrategy: 'leaf',
    tickFilter: null,
    tickable: [
      {
        label: 'Satisfied customers',
        children: [
          {
            label: 'Good food',
            icon: 'restaurant_menu',            
            children: [
              { label: 'Quality ingredients' },
              { label: 'Good recipe' }
            ]
          },
          {
            label: 'Good service',
            icon: 'room_service',
            selected: 'true',
            children: [
              { label: 'Prompt attention' },
              { label: 'Professional waiter' }
            ]
          },
          {
            label: 'Pleasant surroundings',
            icon: 'photo',
            children: [
              {
                label: 'Happy atmosphere (not tickable)',
                tickable: false
              },
              {
                label: 'Good table presentation (disabled node)',
                disabled: true
              },
              {
                label: 'Pleasing decor'
              }
            ]
          },
          {
            label: 'Extra information (has no tick)',
            noTick: true,
            icon: 'photo'
          },
          {
            label: 'Forced tick strategy (to "strict" in this case)',
            tickStrategy: 'strict',
            icon: 'school',
            children: [
              {
                label: 'Happy atmosphere'
              },
              {
                label: 'Good table presentation'
              },
              {
                label: 'Very pleasing decor'
              }
            ]
          }
        ]
      }
    ]
  })
}
</script>
