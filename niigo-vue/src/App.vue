<template>
    <!-- 导航栏 -->
     <nav class="navbar">
        <div class="nav-logo">25:00</div>
        <ul class="nav-links">
          <!-- href="#" 暂时代表不跳转 -->
          <li><a href="#home" class="active">首页</a></li>
          <li><a href="#members">成员介绍</a></li>
          <li><a href="#music">音乐作品</a></li>
          <li><a href="#about">关于我们</a></li>
        </ul>
     </nav>

  <div class="app-container">
    <header id="home" class="section-container">
        <h1>25时，在Nightcord见。</h1>
        <p>25:00, at Nightcord.</p>

        <!-- 新增：画廊容器 -->
        <div class="gallery-wrapper">
          <div class="gallery-track">
            <!-- 循环生成图片 -->
            <img 
              v-for="img in galleryImages" 
              :key="img.id" 
              :src="img.src" 
              alt="25时插画" 
              class="gallery-item"
            >
          </div>
        </div>
    </header>



    <main id="members" class="card-container">
      <!-- v-for 会自动遍历数据生成卡片 -->
      <a 
          class="card" 
          v-for="character in characters" 
          :key="character.id"
          :href="'#' + character.detailId" 
        >
          <h2>{{ character.name }}</h2>
          <p class="role">{{ character.role }}</p>
          <p class="desc">{{ character.desc }}</p>
      </a>
    </main>

        <!-- ======== 新增：专属角色详细介绍区 ======== -->
    <section class="details-wrapper">
      <div 
        v-for="char in characters" 
        :key="'detail-' + char.id" 
        :id="char.detailId" 
        class="char-detail-box"
      >
        <!-- 左侧：多张立绘滑动区 -->
        <div class="char-sprites">
          <img 
            v-for="(sprite, index) in char.sprites" 
            :key="index"
            :src="sprite" 
            alt="角色立绘" 
            class="sprite-img"
          >
        </div>

        <!-- 右侧：详细文字区 -->
        <div class="char-info">
          <h3>{{ char.name }}</h3>
          <span class="info-role">{{ char.role }}</span>
          <p class="info-desc">{{ char.fullDesc }}</p>
        </div>
      </div>
    </section>



    <!-- 音乐作品区域 (占位) -->
    <section id="music" class="section-container">
      <h2 class="section-title">音乐作品</h2>
      <div class="placeholder-box">这里是音乐作品展示区...</div>
    </section>

    <!-- 关于我们区域 (占位) -->
    <section id="about" class="section-container">
      <h2 class="section-title">关于我们</h2>
      <div class="placeholder-box">25时，在Nightcord见。是一个由四名少女组成的匿名音乐团体...</div>
    </section>

  </div>
</template>

<script setup>
import { ref } from 'vue'

// 这里是数据源：只要修改这里，页面会自动更新！
const characters = ref([
  { 
    id: 1, 
    detailId: 'char-kanade', // 锚点 ID
    name: '宵崎奏 (K)', 
    role: '作曲担当', 
    desc: '为了拯救某个人的心，而持续创作着音乐。',
    // 新增：多张立绘数组
    sprites: [
      '',
      ''
    ],
    // 新增：详细长文介绍
    fullDesc: '由于过去的某段经历，奏认为自己必须持续创作能够拯救他人的音乐。她过着日夜颠倒的闭门生活，将所有时间都倾注在作曲上。在「25时，在Nightcord见」中代号为K，是团队的发起人和核心人物。'
  },
  { 
    id: 2, 
    detailId: 'char-mafuyu',
    name: '朝比奈真冬 (Yuki)', 
    role: '作词担当', 
    desc: '在优等生的面具下，失去了自我的少女。',
    sprites: [
      '',
      ''
    ],
    fullDesc: '无论是学习还是运动都完美无缺的优等生，在学校里深受老师和同学的信赖。但实际上，她为了满足母亲的期望而抹杀了真实的自己，导致完全失去了味觉，也感觉不到真正的“温暖”。'
  },
  { 
    id: 3, 
    detailId: 'char-ena',
    name: '东云绘名 (Enanan)', 
    role: '插画担当', 
    desc: '渴望才能，在社交网络上寻求认同。',
    sprites: [
      '',
      ''
    ],
    fullDesc: '父亲是知名画家，但她被父亲评价为“没有画画的才能”。尽管如此，她依然无法放弃绘画。为了寻求认同感，她经常在社交网络上发自拍。脾气有些急躁，但其实非常关心同伴。'
  },
  { 
    id: 4, 
    detailId: 'char-mizuki',
    name: '晓山瑞希 (Amia)', 
    role: 'MV制作担当', 
    desc: '充满谜团的开朗气质，背负着无法言说的秘密。',
    sprites: [
      '',
      ''
    ],
    fullDesc: '喜欢可爱的事物，总是以开朗的性格活跃团队气氛。平时很少去学校，有时会独自在顶楼吃饭。心中隐藏着一个无法对任何人诉说的巨大秘密。'
  }
])

// 新增：画廊图片数据
const galleryImages = ref([
  { id: 1, src: 'https://images.unsplash.com/photo-1618336753974-aae8e0450654?auto=format&fit=crop&w=800&q=80' },
  { id: 2, src: 'https://images.unsplash.com/photo-1550684848-fac1c5b4e853?auto=format&fit=crop&w=800&q=80' },
  { id: 3, src: 'https://images.unsplash.com/photo-1614850523459-c2f4c699c52e?auto=format&fit=crop&w=800&q=80' }
])

</script>

<style scoped>
/* 这里写 CSS。scoped 表示这些样式只在这个组件生效，不会污染其他页面 */
.app-container {
  background-color: #1a1a24;
  min-height: 100vh;
  color: #e0e0e0;
}
header {
  text-align: center;
  padding: 20px 20px 40px 20px;
}
header h1 {
  color: #a493b8;
}
.card-container {
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
  gap: 30px;
}
.card {
  background-color: #242435;
  width: 250px;
  border-radius: 15px;
  padding: 20px;
  text-align: center;
  transition: transform 0.3s;
}
.card:hover {
  transform: translateY(-10px);
}
.role { color: #a493b8; font-weight: bold; margin-bottom: 15px;}

/* --- 新增导航栏样式 --- */

/* 导航栏整体 */
.navbar {
  /* 固定在页面顶部 */
  position: sticky;
  top: 0;
  z-index: 100; /* 确保它在最上层，不会被卡片遮挡 */
  
  /* Flexbox 布局：让 Logo 和 菜单 分列左右两端 */
  display: flex;
  justify-content: space-between;
  align-items: center;
  
  /* 外观设置 */
  background-color: rgba(26, 26, 36, 0.9); /* 半透明背景，更有现代感 */
  backdrop-filter: blur(10px); /* 背景毛玻璃模糊效果 */
  padding: 15px 40px;
  border-bottom: 1px solid #333344;
}

/* 左侧 Logo */
.nav-logo {
  font-size: 1.5rem;
  font-weight: bold;
  color: #ffffff;
  letter-spacing: 2px;
}

/* 右侧菜单列表 */
.nav-links {
  display: flex; /* 让列表项横向排列 */
  gap: 30px;     /* 菜单项之间的间距 */
  list-style: none; /* 去掉默认的小圆点 */
  margin: 0;
  padding: 0;
}

/* 菜单链接文字 */
.nav-links a {
  color: #aaaaaa;
  text-decoration: none; /* 去掉下划线 */
  font-size: 1rem;
  transition: color 0.3s ease; /* 颜色渐变动画 */
}

/* 鼠标悬浮和激活状态的文字颜色（25时的紫色） */
.nav-links a:hover,
.nav-links a.active {
  color: #a493b8;
}

/* 新增区域的基础排版 */
.section-container {
  padding: 40px 20px;
  min-height: 50vh; /* 让每个区域至少占屏幕一半高度，方便测试滚动 */
}

.section-title {
  text-align: center;
  color: #ffffff;
  margin-bottom: 30px;
  font-size: 2rem;
}

.placeholder-box {
  background-color: #242435;
  color: #aaaaaa;
  padding: 50px;
  text-align: center;
  border-radius: 15px;
  max-width: 800px;
  margin: 0 auto;
}

/* --- 画廊样式 --- */

/* 画廊外层容器，用来居中和限制最大宽度 */
.gallery-wrapper {
  max-width: 800px;
  margin: 40px auto 0; /* 距离上方标题 40px，左右居中 */
  padding: 0 20px;
}

/* 核心：滑动轨道 */
.gallery-track {
  display: flex; /* 让图片横向排队 */
  gap: 20px; /* 图片之间的间距 */
  overflow-x: auto; /* 允许横向滚动 */
  padding-bottom: 15px; /* 给下方的滚动条留出一点空间 */
  
  /* 魔法属性：开启滚动捕捉功能 */
  scroll-snap-type: x mandatory; 
}

/* 隐藏浏览器默认的丑陋滚动条，换成25时风格的紫色滚动条（仅对 Webkit 内核浏览器有效） */
.gallery-track::-webkit-scrollbar {
  height: 8px;
}
.gallery-track::-webkit-scrollbar-track {
  background: #242435;
  border-radius: 10px;
}
.gallery-track::-webkit-scrollbar-thumb {
  background: #a493b8; /* 25时的紫色 */
  border-radius: 10px;
}

/* 单张图片样式 */
.gallery-item {
  flex: 0 0 85%; /* 关键：每张图占据宽度的85%，这样能露出下一张图的一小截，暗示用户可以滑动 */
  height: 300px; /* 图片固定高度 */
  object-fit: cover; /* 保证图片不会被拉伸变形，而是等比例裁剪填满 */
  border-radius: 15px; /* 圆角 */
  box-shadow: 0 8px 16px rgba(0, 0, 0, 0.4); /* 阴影增加立体感 */
  
  /* 魔法属性：每次滑动停下时，图片要乖乖停在中央 */
  scroll-snap-align: center; 
}

/* 适配大屏幕，在大屏幕上图片可以宽一点 */
@media (min-width: 768px) {
  .gallery-item {
    flex: 0 0 100%; /* 电脑屏幕上每张图占满 100% 宽度 */
    height: 400px;
  }
}

/* --- 因为把卡片改成了a标签，需要取消默认的下划线和颜色 --- */
a.card {
  text-decoration: none;
  display: block; 
  cursor: pointer;
  
  /* 新增这两行，强制覆盖默认颜色 */
  color: inherit; 
  -webkit-tap-highlight-color: transparent; /* 去除手机端点击时闪烁的高亮背景 */
}

/* 确保 a 标签内部的所有文字都不受默认链接颜色的影响 */
a.card h2,
a.card .role,
a.card .desc {
  /* 确保文字颜色依然使用我们在 HTML/CSS 里设定的颜色 */
  transition: color 0.3s ease;
}

/* --- 角色详细介绍区整体样式 --- */
.details-wrapper {
  max-width: 900px;
  margin: 0 auto;
  padding: 20px;
}

/* 每个角色的详情盒子 */
.char-detail-box {
  display: flex; /* 开启 Flexbox 左右布局 */
  gap: 40px; /* 左右间距 */
  background-color: #242435;
  border-radius: 20px;
  padding: 30px;
  margin-bottom: 50px; /* 每个角色盒子之间的间距 */
}

/* --- 左侧立绘滑动区 --- */
.char-sprites {
  flex: 0 0 350px; /* 固定左侧宽度为 350px */
  display: flex;
  overflow-x: auto; /* 允许左右滑动 */
  scroll-snap-type: x mandatory; /* 开启滑动捕捉 */
  border-radius: 15px;
}

/* 隐藏立绘滑动区的滚动条 */
.char-sprites::-webkit-scrollbar {
  display: none; 
}

.sprite-img {
  flex: 0 0 100%; /* 每张图片占满宽度，这样一次只显示一张 */
  height: 450px;
  object-fit: cover;
  scroll-snap-align: center; /* 滑动时对齐中心 */
}

/* --- 右侧文字信息区 --- */
.char-info {
  flex: 1; /* 占据剩下的所有空间 */
  display: flex;
  flex-direction: column;
  justify-content: center; /* 文字垂直居中 */
}

.char-info h3 {
  font-size: 2rem;
  color: #ffffff;
  margin-bottom: 10px;
}

.info-role {
  display: inline-block;
  background-color: #a493b8;
  color: #1a1a24;
  padding: 5px 15px;
  border-radius: 20px;
  font-weight: bold;
  font-size: 0.9rem;
  margin-bottom: 20px;
  width: fit-content;
}

.info-desc {
  color: #cccccc;
  line-height: 1.8;
  font-size: 1.05rem;
}

/* --- 响应式适配：如果是手机屏幕，变成上下布局 --- */
@media (max-width: 768px) {
  .char-detail-box {
    flex-direction: column; /* 改为上下排列 */
    padding: 20px;
  }
  .char-sprites {
    flex: auto;
    width: 100%;
  }
}


</style>
