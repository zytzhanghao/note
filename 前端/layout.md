圣杯布局：
div 父
  div中
  div左
  div右
思路：中宽100% 中左右都有浮动，float：left 保证div水平布局
父 设定左右margin 留出位置 左右也设置margin 保证同一行
用定位进行左右位置调整。
注：父也要设置高度。解决高度崩塌
双飞翼布局：
div 父
  div中
    div inner
  div左
  div右
思路：去掉父样式 去掉双飞翼的定位，发现成中包含左右三列布局
通过inner margin左右 呈现独立三列布局