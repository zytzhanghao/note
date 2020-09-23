P19034 00SDS ARM様向け タフネスシステム刷新(日本)
简介：是一款toC的员工心里健康测试系统。前端部分分为俩个端，从业员端，和管理端。

路由系统：多页系统，由菜单控制。所有菜单首页都是菜单系统
   {
      path: '/',
      name: 'home',
      component: Layout,  //菜单系统，最外层
      meta: { title: '' },
      children: [
        {
          path: '/',
          name: 'dashboard',
          meta: { title: '' },
          component: () => import('@/components/home')
        },
        {
          path: '/contracts',
          name: 'contracts',
          meta: { title: '契約選択ー' },
          component: () => import('@/components/common/ContractsSelect')
        }
      ]
    },
权限控制系统：