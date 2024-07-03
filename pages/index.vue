<template>
  <div class="grid gap-2">
    <header class="flex items-start justify-between">
      <div class="grow">
        <p>Welcome back Basem Ahmed !</p>
        <h1>Dashboard</h1>
      </div>
      <div class="bg-neutral-200 h-[36px] w-[120px]"></div>
    </header>

    <main>
      <Tabs
        default-value="Today"
        @click="setCategory"
        class="w-[calc(100vw-4rem)] lg:w-[100%]">
        <TabsList>
          <TabsTrigger
            v-for="(item, index) in list"
            :key="index"
            :value="item.title">
            {{ item.title }}
          </TabsTrigger>
        </TabsList>
        <TabsContent
          v-for="(item, index) in list"
          :key="index"
          :value="item.title">
          <!-- <component :is="item.component" /> -->
          <highchart :options="options" />
        </TabsContent>
      </Tabs>

      <section>Chart</section>
    </main>

    <footer>i will have 3 different cards</footer>
  </div>
</template>

<script setup lang="ts">
import { Tabs, TabsContent, TabsList, TabsTrigger } from '@/components/ui/tabs';
const list = [
  {
    title: 'Today',
    component: resolveComponent('TabsToday'),
  },
  {
    title: 'Week',
    component: '<div>Week</div>',
  },
  {
    title: 'Month',
    component: '<div>Month</div>',
  },
  {
    title: 'Year',
    component: '<div>Year</div>',
  },
];

let categories = ref({
  today: [
    "00:00", "01:00", "02:00", "03:00", "04:00", "05:00",
    "06:00", "07:00", "08:00", "09:00", "10:00", "11:00",
    "12:00", "13:00", "14:00", "15:00", "16:00", "17:00",
    "18:00", "19:00", "20:00", "21:00", "22:00", "23:00"
  ],
  week: [
    "Sunday", "Monday", "Tuesday", "Wednesday", 
    "Thursday", "Friday", "Saturday"
  ],
  month: Array.from({ length: 30 }, (_, i) => `${i + 1}`),
  year: [
    "January", "February", "March", "April", 
    "May", "June", "July", "August", 
    "September", "October", "November", "December"
  ],
});

let currentCategory = ref('today');

const options = computed(() => ({
  chart: {
    type: 'line',
    animation: {
      enabled: false,
    },
  },
  legend: {
    enabled: false,
  },
  title: {
    text: '',
  },
  xAxis: {
    gridLineColor: 'transparent',
    categories: categories.value[currentCategory.value as keyof typeof categories.value],
  },
  yAxis: {
    gridLineColor: 'transparent',
    title: {
      text: '',
    },
  },
  plotOptions: {
    line: {
      marker: {
        enabled: false,
      },
      dataLabels: {
        enabled: true,
      },
      enableMouseTracking: false,
    },
  },
  series: [
    {
      name: 'line',
      lineWidth: '4px',
      color: {
        linearGradient: {},
        stops: [
          [0, 'rgba(255, 176, 69, 1)'],
          [0.33, 'rgba(253, 29, 29, 1)'],
          [0.66, 'rgba(131, 58, 180, 1)'],
          [1, 'rgba(29, 217, 93, 1)'],

        ]
      },
      data: [
        16.0, 18.2, 23.1, 27.9, 32.2, 36.4, 39.8, 38.4, 35.5, 29.2, 22.0, 17.8,
      ],
    },
  ],
}));

function generateRandomNumbers(number : number) {
    let randomNumbers = [];
    for (let i = 0; i < number; i++) {
        randomNumbers.push(Math.floor(Math.random() * 100) + 1);
    }
    console.log(randomNumbers);
    return randomNumbers;
}

const setCategory = (e: MouseEvent) => {
  let v = (e.target as HTMLElement).innerText.toLowerCase();
  currentCategory.value = v;
  switch (v) {
    case 'today':
      options.value.series[0].data = generateRandomNumbers(24);
      break;
    case 'week':
      options.value.series[0].data = generateRandomNumbers(7);
      break;
    case 'month':
      options.value.series[0].data = generateRandomNumbers(12);
      break;
    case 'year':
      options.value.series[0].data = generateRandomNumbers(12);
      break;
    default:
      options.value.series[0].data = generateRandomNumbers(24);
      break;
  }
};

// Hook to generate random numbers on component mount
onMounted(() => {
    // Assuming you want to generate random numbers for initial data
    options.value.series[0].data = generateRandomNumbers(7);
});
</script>

<style scoped></style>
