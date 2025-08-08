<script setup lang="ts">
import { onMounted, onUnmounted } from 'vue'
import gsap from 'gsap'

// 定义点的类型
interface Dot {
  x: number
  y: number
  size: number
  speed: number
  angle: number
}

let animationContext: any = null

onMounted(() => {
  // 创建网格背景
  const canvas = document.createElement('canvas')
  canvas.id = 'grid-canvas'
  canvas.style.cssText = `
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    z-index: -1;
    pointer-events: none;
  `
  document.body.appendChild(canvas)

  const ctx = canvas.getContext('2d')
  if (!ctx) return

  const resizeCanvas = () => {
    canvas.width = window.innerWidth
    canvas.height = window.innerHeight
  }

  window.addEventListener('resize', resizeCanvas)
  resizeCanvas()

  const gridSize = 50
  const lineWidth = 0.5
  const lineColor = 'rgba(0, 0, 0, 0.1)'

  let time = 0
  const dots: Dot[] = []
  const dotCount = 50

  for (let i = 0; i < dotCount; i++) {
    dots.push({
      x: Math.random() * canvas.width,
      y: Math.random() * canvas.height,
      size: Math.random() * 3 + 1,
      speed: Math.random() * 0.5 + 0.1,
      angle: Math.random() * Math.PI * 2,
    })
  }

  const draw = () => {
    if (!ctx) return

    ctx.clearRect(0, 0, canvas.width, canvas.height)

    ctx.strokeStyle = lineColor
    ctx.lineWidth = lineWidth

    for (let x = 0; x <= canvas.width; x += gridSize) {
      ctx.beginPath()
      ctx.moveTo(x, 0)
      ctx.lineTo(x, canvas.height)
      ctx.stroke()
    }

    for (let y = 0; y <= canvas.height; y += gridSize) {
      ctx.beginPath()
      ctx.moveTo(0, y)
      ctx.lineTo(canvas.width, y)
      ctx.stroke()
    }

    time += 0.01
    dots.forEach((dot) => {
      dot.x += Math.cos(dot.angle) * dot.speed
      dot.y += Math.sin(dot.angle) * dot.speed

      if (dot.x < 0 || dot.x > canvas.width) dot.angle = Math.PI - dot.angle
      if (dot.y < 0 || dot.y > canvas.height) dot.angle = -dot.angle

      ctx.beginPath()
      ctx.arc(dot.x, dot.y, dot.size, 0, Math.PI * 2)
      ctx.fillStyle = 'rgba(0, 123, 255, 0.7)'
      ctx.fill()
    })

    for (let i = 0; i < dots.length; i++) {
      for (let j = i + 1; j < dots.length; j++) {
        const dx = dots[i].x - dots[j].x
        const dy = dots[i].y - dots[j].y
        const distance = Math.sqrt(dx * dx + dy * dy)

        if (distance < 100) {
          ctx.beginPath()
          ctx.moveTo(dots[i].x, dots[i].y)
          ctx.lineTo(dots[j].x, dots[j].y)
          ctx.strokeStyle = `rgba(0, 123, 255, ${0.3 * (1 - distance / 100)})`
          ctx.lineWidth = 1
          ctx.stroke()
        }
      }
    }

    animationContext = requestAnimationFrame(draw)
  }

  draw()

  gsap.to(dots, {
    duration: 10,
    ease: 'none',
    onComplete: function () {
      gsap.to(dots, {
        duration: 10,
        ease: 'none',
      })
    },
  })
})

onUnmounted(() => {
  if (animationContext) {
    cancelAnimationFrame(animationContext)
  }
  const canvas = document.getElementById('grid-canvas')
  if (canvas) {
    canvas.remove()
  }
})
</script>
<template>
  <div class="home-view">
    <div class="hero">
      <div class="content">
        <h2>SimpleSSH</h2>
        <h1>
          简洁美观的
          <span class="gradient-text">SSH客户端</span>
        </h1>
        <p>
          SimpleSSH 是一个基于 Fluent 设计语言，使用 WPF 构建的 SSH 客户端，<br />适用于 Windows
          系列操作系统，使用 GPL3.0 在 GitHub 开放源代码。
        </p>
      </div>
      <div class="buttons">
        <el-button size="large" type="primary" round>
          <svg
            t="1754625061241"
            class="icon"
            viewBox="0 0 1024 1024"
            version="1.1"
            xmlns="http://www.w3.org/2000/svg"
            p-id="6264"
            width="200"
            height="200"
          >
            <path
              d="M896 672c-17.066667 0-32 14.933333-32 32v128c0 6.4-4.266667 10.666667-10.666667 10.666667H170.666667c-6.4 0-10.666667-4.266667-10.666667-10.666667v-128c0-17.066667-14.933333-32-32-32s-32 14.933333-32 32v128c0 40.533333 34.133333 74.666667 74.666667 74.666667h682.666666c40.533333 0 74.666667-34.133333 74.666667-74.666667v-128c0-17.066667-14.933333-32-32-32z"
              fill="#ffffff"
              p-id="6265"
            ></path>
            <path
              d="M488.533333 727.466667c6.4 6.4 14.933333 8.533333 23.466667 8.533333s17.066667-2.133333 23.466667-8.533333l213.333333-213.333334c12.8-12.8 12.8-32 0-44.8-12.8-12.8-32-12.8-44.8 0l-157.866667 157.866667V170.666667c0-17.066667-14.933333-32-32-32s-34.133333 14.933333-34.133333 32v456.533333L322.133333 469.333333c-12.8-12.8-32-12.8-44.8 0-12.8 12.8-12.8 32 0 44.8l211.2 213.333334z"
              fill="#ffffff"
              p-id="6266"
            ></path>
          </svg>
          下载
        </el-button>
        <el-button size="large" type="info" style="background-color: #333; color: #fff" round>
          <svg
            t="1754625148808"
            class="icon"
            viewBox="0 0 1024 1024"
            version="1.1"
            xmlns="http://www.w3.org/2000/svg"
            p-id="8169"
            width="200"
            height="200"
          >
            <path
              d="M511.6 76.3C264.3 76.2 64 276.4 64 523.5 64 718.9 189.3 885 363.8 946c23.5 5.9 19.9-10.8 19.9-22.2v-77.5c-135.7 15.9-141.2-73.9-150.3-88.9C215 726 171.5 718 184.5 703c30.9-15.9 62.4 4 98.9 57.9 26.4 39.1 77.9 32.5 104 26 5.7-23.5 17.9-44.5 34.7-60.8-140.6-25.2-199.2-111-199.2-213 0-49.5 16.3-95 48.3-131.7-20.4-60.5 1.9-112.3 4.9-120 58.1-5.2 118.5 41.6 123.2 45.3 33-8.9 70.7-13.6 112.9-13.6 42.4 0 80.2 4.9 113.5 13.9 11.3-8.6 67.3-48.8 121.3-43.9 2.9 7.7 24.7 58.3 5.5 118 32.4 36.8 48.9 82.7 48.9 132.3 0 102.2-59 188.1-200 212.9 23.5 23.2 38.1 55.4 38.1 91v112.5c0.8 9 0 17.9 15 17.9 177.1-59.7 304.6-227 304.6-424.1 0-247.2-200.4-447.3-447.5-447.3z"
              p-id="8170"
              fill="#ffffff"
            ></path>
          </svg>
          GitHub
        </el-button>
      </div>
    </div>
  </div>
</template>
<style scoped>
.hero {
  background-size: cover;
  background-position: center;
  height: 100vh;
  display: flex;
  align-items: center;
  justify-content: center;
  flex-direction: column;
}

.content {
  text-align: center;
  h1 {
    font-size: 3.5rem;
    display: flex;
    align-items: center;
    justify-content: center;
    gap: 0.5rem;
  }

  h2 {
    font-size: 30px;
    margin-bottom: -2rem;
  }

  p {
    font-size: 20px;
    margin-bottom: 2rem;
  }
}

.buttons {
  flex-direction: column;
  gap: 1rem;
  align-items: center;
}

.gradient-text {
  background: linear-gradient(45deg, #00c6ff, #c802ff);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
  animation: gradientShift 3s ease infinite;
  background-size: 200% 200%;
}
.icon {
  height: 20px;
  width: 20px;
  margin-right: 3px;
}
</style>
