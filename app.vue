<template>
  <div class="min-h-screen">
    <div class="min-h-screen bg-gray-50 dark:bg-gray-900">
      <header class="bg-white dark:bg-gray-800 shadow-sm border-b border-gray-200 dark:border-gray-700">
        <nav class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 h-16 flex items-center justify-between">
          <div class="flex items-center space-x-4">
            <div class="w-8 h-8 bg-gradient-to-r from-blue-500 to-purple-600 rounded-lg flex items-center justify-center">
              <svg class="w-5 h-5 text-white" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 19v-6a2 2 0 00-2-2H5a2 2 0 00-2 2v6a2 2 0 002 2h2a2 2 0 002-2zm0 0V9a2 2 0 012-2h2a2 2 0 012 2v10m-6 0a2 2 0 002 2h2a2 2 0 002-2m0 0V5a2 2 0 012-2h2a2 2 0 012 2v14a2 2 0 01-2 2h-2a2 2 0 01-2-2z"></path>
              </svg>
            </div>
            <h1 class="text-xl font-bold text-gray-900 dark:text-white">Analytics Dashboard</h1>
          </div>
          <div class="flex items-center space-x-4">
            <div class="flex space-x-4">
              <a href="#overview" class="text-gray-600 dark:text-gray-300 hover:text-gray-900 dark:hover:text-white transition-colors">Overview</a>
              <a href="#analytics" class="text-gray-600 dark:text-gray-300 hover:text-gray-900 dark:hover:text-white transition-colors">Analytics</a>
              <a href="#reports" class="text-gray-600 dark:text-gray-300 hover:text-gray-900 dark:hover:text-white transition-colors">Reports</a>
            </div>
            <ClientOnly>
              <button @click="toggleDark()" class="p-2 text-gray-500 dark:text-gray-400 hover:text-gray-900 dark:hover:text-white transition-colors rounded-lg hover:bg-gray-100 dark:hover:bg-gray-700">
                <span v-if="isDark">🌞</span>
                <span v-else>🌙</span>
              </button>
            </ClientOnly>
          </div>
        </nav>
      </header>

      <main class="max-w-7xl mx-auto py-6 px-4 sm:px-6 lg:px-8">
        <!-- Key Metrics -->
        <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-4 gap-6 mb-8">
          <div class="bg-white dark:bg-gray-800 rounded-xl shadow-sm border border-gray-200 dark:border-gray-700 p-6 hover:shadow-md transition-shadow">
            <div class="flex items-center justify-between">
              <div>
                <p class="text-sm font-medium text-gray-600 dark:text-gray-400">Total Revenue</p>
                <p class="text-3xl font-bold text-gray-900 dark:text-white">${{ formatNumber(metrics.totalRevenue) }}</p>
                <p class="text-sm text-green-600 dark:text-green-400 flex items-center mt-1">
                  <svg class="w-4 h-4 mr-1" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M7 17l9.2-9.2M17 17V7H7"></path>
                  </svg>
                  +12.5%
                </p>
              </div>
              <div class="w-12 h-12 bg-green-100 dark:bg-green-900 rounded-lg flex items-center justify-center">
                <svg class="w-6 h-6 text-green-600 dark:text-green-400" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                  <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 8c-1.657 0-3 .895-3 2s1.343 2 3 2 3 .895 3 2-1.343 2-3 2m0-8c1.11 0 2.08.402 2.599 1M12 8V7m0 1v8m0 0v1m0-1c-1.11 0-2.08-.402-2.599-1"></path>
                </svg>
              </div>
            </div>
          </div>

          <div class="bg-white dark:bg-gray-800 rounded-xl shadow-sm border border-gray-200 dark:border-gray-700 p-6 hover:shadow-md transition-shadow">
            <div class="flex items-center justify-between">
              <div>
                <p class="text-sm font-medium text-gray-600 dark:text-gray-400">Active Users</p>
                <p class="text-3xl font-bold text-gray-900 dark:text-white">{{ formatNumber(metrics.activeUsers) }}</p>
                <p class="text-sm text-blue-600 dark:text-blue-400 flex items-center mt-1">
                  <svg class="w-4 h-4 mr-1" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M7 17l9.2-9.2M17 17V7H7"></path>
                  </svg>
                  +8.2%
                </p>
              </div>
              <div class="w-12 h-12 bg-blue-100 dark:bg-blue-900 rounded-lg flex items-center justify-center">
                <svg class="w-6 h-6 text-blue-600 dark:text-blue-400" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                  <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 4.354a4 4 0 110 5.292M15 21H3v-1a6 6 0 0112 0v1zm0 0h6v-1a6 6 0 00-9-5.197m13.5-9a2.5 2.5 0 11-5 0 2.5 2.5 0 015 0z"></path>
                </svg>
              </div>
            </div>
          </div>

          <div class="bg-white dark:bg-gray-800 rounded-xl shadow-sm border border-gray-200 dark:border-gray-700 p-6 hover:shadow-md transition-shadow">
            <div class="flex items-center justify-between">
              <div>
                <p class="text-sm font-medium text-gray-600 dark:text-gray-400">Conversion Rate</p>
                <p class="text-3xl font-bold text-gray-900 dark:text-white">{{ metrics.conversionRate }}%</p>
                <p class="text-sm text-purple-600 dark:text-purple-400 flex items-center mt-1">
                  <svg class="w-4 h-4 mr-1" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M7 17l9.2-9.2M17 17V7H7"></path>
                  </svg>
                  +3.1%
                </p>
              </div>
              <div class="w-12 h-12 bg-purple-100 dark:bg-purple-900 rounded-lg flex items-center justify-center">
                <svg class="w-6 h-6 text-purple-600 dark:text-purple-400" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                  <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 19v-6a2 2 0 00-2-2H5a2 2 0 00-2 2v6a2 2 0 002 2h2a2 2 0 002-2zm0 0V9a2 2 0 012-2h2a2 2 0 012 2v10m-6 0a2 2 0 002 2h2a2 2 0 002-2m0 0V5a2 2 0 012-2h2a2 2 0 012 2v14a2 2 0 01-2 2h-2a2 2 0 01-2-2z"></path>
                </svg>
              </div>
            </div>
          </div>

          <div class="bg-white dark:bg-gray-800 rounded-xl shadow-sm border border-gray-200 dark:border-gray-700 p-6 hover:shadow-md transition-shadow">
            <div class="flex items-center justify-between">
              <div>
                <p class="text-sm font-medium text-gray-600 dark:text-gray-400">Avg. Order Value</p>
                <p class="text-3xl font-bold text-gray-900 dark:text-white">${{ metrics.avgOrderValue }}</p>
                <p class="text-sm text-orange-600 dark:text-orange-400 flex items-center mt-1">
                  <svg class="w-4 h-4 mr-1" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M7 17l9.2-9.2M17 17V7H7"></path>
                  </svg>
                  +5.7%
                </p>
              </div>
              <div class="w-12 h-12 bg-orange-100 dark:bg-orange-900 rounded-lg flex items-center justify-center">
                <svg class="w-6 h-6 text-orange-600 dark:text-orange-400" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                  <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M16 11V7a4 4 0 00-8 0v4M5 9h14l1 12H4L5 9z"></path>
                </svg>
              </div>
            </div>
          </div>
        </div>

        <!-- Charts Grid -->
        <div class="grid grid-cols-1 lg:grid-cols-2 gap-6 mb-8">
          <!-- Revenue Chart -->
          <div class="bg-white dark:bg-gray-800 rounded-xl shadow-sm border border-gray-200 dark:border-gray-700 p-6">
            <div class="flex items-center justify-between mb-6">
              <h3 class="text-lg font-semibold text-gray-900 dark:text-white">Revenue Trend</h3>
              <select class="text-sm border border-gray-300 dark:border-gray-600 rounded-lg px-3 py-1 bg-white dark:bg-gray-700 text-gray-900 dark:text-white">
                <option>Last 7 days</option>
                <option>Last 30 days</option>
                <option>Last 90 days</option>
              </select>
            </div>
            <div class="h-80">
              <LineChart :data="revenueChartData" :options="chartOptions" />
            </div>
          </div>

          <!-- User Analytics -->
          <div class="bg-white dark:bg-gray-800 rounded-xl shadow-sm border border-gray-200 dark:border-gray-700 p-6">
            <div class="flex items-center justify-between mb-6">
              <h3 class="text-lg font-semibold text-gray-900 dark:text-white">User Analytics</h3>
              <div class="flex space-x-2">
                <button class="px-3 py-1 text-sm bg-blue-100 dark:bg-blue-900 text-blue-700 dark:text-blue-300 rounded-lg">New</button>
                <button class="px-3 py-1 text-sm text-gray-600 dark:text-gray-400 hover:bg-gray-100 dark:hover:bg-gray-700 rounded-lg">Returning</button>
              </div>
            </div>
            <div class="h-80">
              <BarChart :data="userChartData" :options="chartOptions" />
            </div>
          </div>
        </div>

        <!-- Additional Charts -->
        <div class="grid grid-cols-1 lg:grid-cols-3 gap-6 mb-8">
          <!-- Traffic Sources -->
          <div class="bg-white dark:bg-gray-800 rounded-xl shadow-sm border border-gray-200 dark:border-gray-700 p-6">
            <h3 class="text-lg font-semibold text-gray-900 dark:text-white mb-6">Traffic Sources</h3>
            <div class="h-64">
              <DoughnutChart :data="trafficSourcesData" :options="doughnutOptions" />
            </div>
          </div>

          <!-- Performance Metrics -->
          <div class="bg-white dark:bg-gray-800 rounded-xl shadow-sm border border-gray-200 dark:border-gray-700 p-6">
            <h3 class="text-lg font-semibold text-gray-900 dark:text-white mb-6">Performance</h3>
            <div class="space-y-4">
              <div v-for="metric in performanceMetrics" :key="metric.name" class="flex items-center justify-between">
                <div class="flex items-center space-x-3">
                  <div :class="metric.color" class="w-3 h-3 rounded-full"></div>
                  <span class="text-sm text-gray-600 dark:text-gray-400">{{ metric.name }}</span>
                </div>
                <div class="flex items-center space-x-2">
                  <span class="text-sm font-medium text-gray-900 dark:text-white">{{ metric.value }}</span>
                  <div class="w-16 h-2 bg-gray-200 dark:bg-gray-700 rounded-full">
                    <div :class="metric.color" :style="`width: ${metric.percentage}%`" class="h-2 rounded-full"></div>
                  </div>
                </div>
              </div>
            </div>
          </div>

          <!-- Recent Activity -->
          <div class="bg-white dark:bg-gray-800 rounded-xl shadow-sm border border-gray-200 dark:border-gray-700 p-6">
            <h3 class="text-lg font-semibold text-gray-900 dark:text-white mb-6">Recent Activity</h3>
            <div class="space-y-4">
              <div v-for="activity in recentActivities" :key="activity.id" class="flex items-start space-x-3">
                <div :class="activity.color" class="w-2 h-2 rounded-full mt-2"></div>
                <div class="flex-1 min-w-0">
                  <p class="text-sm text-gray-900 dark:text-white">{{ activity.description }}</p>
                  <p class="text-xs text-gray-500 dark:text-gray-400">{{ activity.time }}</p>
                </div>
              </div>
            </div>
          </div>
        </div>

        <!-- Data Table -->
        <div class="bg-white dark:bg-gray-800 rounded-xl shadow-sm border border-gray-200 dark:border-gray-700">
          <div class="px-6 py-4 border-b border-gray-200 dark:border-gray-700">
            <div class="flex items-center justify-between">
              <h3 class="text-lg font-semibold text-gray-900 dark:text-white">Top Performing Pages</h3>
              <button class="text-sm text-blue-600 dark:text-blue-400 hover:text-blue-800 dark:hover:text-blue-300">View All</button>
            </div>
          </div>
          <div class="overflow-x-auto">
            <table class="min-w-full divide-y divide-gray-200 dark:divide-gray-700">
              <thead class="bg-gray-50 dark:bg-gray-900">
                <tr>
                  <th class="px-6 py-3 text-left text-xs font-medium text-gray-500 dark:text-gray-400 uppercase tracking-wider">Page</th>
                  <th class="px-6 py-3 text-left text-xs font-medium text-gray-500 dark:text-gray-400 uppercase tracking-wider">Views</th>
                  <th class="px-6 py-3 text-left text-xs font-medium text-gray-500 dark:text-gray-400 uppercase tracking-wider">Unique Visitors</th>
                  <th class="px-6 py-3 text-left text-xs font-medium text-gray-500 dark:text-gray-400 uppercase tracking-wider">Bounce Rate</th>
                  <th class="px-6 py-3 text-left text-xs font-medium text-gray-500 dark:text-gray-400 uppercase tracking-wider">Avg. Time</th>
                </tr>
              </thead>
              <tbody class="bg-white dark:bg-gray-800 divide-y divide-gray-200 dark:divide-gray-700">
                <tr v-for="page in topPages" :key="page.path" class="hover:bg-gray-50 dark:hover:bg-gray-700">
                  <td class="px-6 py-4 whitespace-nowrap text-sm font-medium text-gray-900 dark:text-white">{{ page.path }}</td>
                  <td class="px-6 py-4 whitespace-nowrap text-sm text-gray-500 dark:text-gray-400">{{ formatNumber(page.views) }}</td>
                  <td class="px-6 py-4 whitespace-nowrap text-sm text-gray-500 dark:text-gray-400">{{ formatNumber(page.uniqueVisitors) }}</td>
                  <td class="px-6 py-4 whitespace-nowrap text-sm text-gray-500 dark:text-gray-400">{{ page.bounceRate }}%</td>
                  <td class="px-6 py-4 whitespace-nowrap text-sm text-gray-500 dark:text-gray-400">{{ page.avgTime }}</td>
                </tr>
              </tbody>
            </table>
          </div>
        </div>
      </main>
    </div>
  </div>
</template>

<script setup>
import { useDark, useToggle } from '@vueuse/core'
import { ref, onMounted } from 'vue'
import { format, subDays } from 'date-fns'

const isDark = useDark()
const toggleDark = useToggle(isDark)

// Reactive data
const metrics = ref({
  totalRevenue: 847250,
  activeUsers: 12847,
  conversionRate: 3.24,
  avgOrderValue: 156
})

const performanceMetrics = ref([
  { name: 'Page Load Speed', value: '1.2s', percentage: 85, color: 'bg-green-500' },
  { name: 'Server Response', value: '245ms', percentage: 92, color: 'bg-blue-500' },
  { name: 'First Paint', value: '0.8s', percentage: 78, color: 'bg-yellow-500' },
  { name: 'Time to Interactive', value: '2.1s', percentage: 88, color: 'bg-purple-500' }
])

const recentActivities = ref([
  { id: 1, description: 'New user registered from organic search', time: '2 minutes ago', color: 'bg-green-500' },
  { id: 2, description: 'Payment processed for order #12847', time: '5 minutes ago', color: 'bg-blue-500' },
  { id: 3, description: 'High traffic spike detected on /products', time: '12 minutes ago', color: 'bg-yellow-500' },
  { id: 4, description: 'Weekly report generated successfully', time: '1 hour ago', color: 'bg-purple-500' },
  { id: 5, description: 'Database backup completed', time: '2 hours ago', color: 'bg-gray-500' }
])

const topPages = ref([
  { path: '/dashboard', views: 45672, uniqueVisitors: 32145, bounceRate: 23.4, avgTime: '3:24' },
  { path: '/products', views: 38291, uniqueVisitors: 28934, bounceRate: 31.2, avgTime: '2:47' },
  { path: '/analytics', views: 29847, uniqueVisitors: 21456, bounceRate: 18.9, avgTime: '4:12' },
  { path: '/settings', views: 18293, uniqueVisitors: 15672, bounceRate: 42.1, avgTime: '1:58' },
  { path: '/reports', views: 12847, uniqueVisitors: 9834, bounceRate: 28.7, avgTime: '3:01' }
])

// Chart data
const revenueChartData = ref({
  labels: [],
  datasets: [{
    label: 'Revenue',
    data: [],
    borderColor: 'rgb(59, 130, 246)',
    backgroundColor: 'rgba(59, 130, 246, 0.1)',
    tension: 0.4,
    fill: true
  }]
})

const userChartData = ref({
  labels: [],
  datasets: [{
    label: 'New Users',
    data: [],
    backgroundColor: 'rgba(34, 197, 94, 0.8)',
    borderColor: 'rgb(34, 197, 94)',
    borderWidth: 1
  }]
})

const trafficSourcesData = ref({
  labels: ['Organic Search', 'Direct', 'Social Media', 'Email', 'Referral'],
  datasets: [{
    data: [45, 25, 15, 10, 5],
    backgroundColor: [
      'rgba(59, 130, 246, 0.8)',
      'rgba(34, 197, 94, 0.8)',
      'rgba(251, 191, 36, 0.8)',
      'rgba(239, 68, 68, 0.8)',
      'rgba(168, 85, 247, 0.8)'
    ],
    borderWidth: 0
  }]
})

// Chart options
const chartOptions = ref({
  responsive: true,
  maintainAspectRatio: false,
  plugins: {
    legend: {
      display: false
    }
  },
  scales: {
    y: {
      beginAtZero: true,
      grid: {
        color: 'rgba(156, 163, 175, 0.1)'
      },
      ticks: {
        color: 'rgba(156, 163, 175, 0.8)'
      }
    },
    x: {
      grid: {
        color: 'rgba(156, 163, 175, 0.1)'
      },
      ticks: {
        color: 'rgba(156, 163, 175, 0.8)'
      }
    }
  }
})

const doughnutOptions = ref({
  responsive: true,
  maintainAspectRatio: false,
  plugins: {
    legend: {
      position: 'bottom',
      labels: {
        padding: 20,
        usePointStyle: true,
        color: 'rgba(156, 163, 175, 0.8)'
      }
    }
  }
})

// Generate sample data
const generateChartData = () => {
  const days = 7
  const labels = []
  const revenueData = []
  const userData = []

  for (let i = days - 1; i >= 0; i--) {
    const date = subDays(new Date(), i)
    labels.push(format(date, 'MMM dd'))
    revenueData.push(Math.floor(Math.random() * 50000) + 30000)
    userData.push(Math.floor(Math.random() * 2000) + 1000)
  }

  revenueChartData.value.labels = labels
  revenueChartData.value.datasets[0].data = revenueData
  userChartData.value.labels = labels
  userChartData.value.datasets[0].data = userData
}

// Utility functions
const formatNumber = (num) => {
  return new Intl.NumberFormat().format(num)
}

// Simulate real-time updates
const updateMetrics = () => {
  setInterval(() => {
    metrics.value.activeUsers += Math.floor(Math.random() * 10) - 5
    metrics.value.totalRevenue += Math.floor(Math.random() * 1000) - 500
  }, 5000)
}

onMounted(() => {
  generateChartData()
  updateMetrics()
})
</script>

<style>
body {
  font-family: 'Inter', sans-serif;
}

.dark {
  color-scheme: dark;
}
</style>