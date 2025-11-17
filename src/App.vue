<template>
  <main class="app-shell gradient-border">
    <div>
      <section class="section" style="padding-bottom: 32px">
        <header class="hero">
          <div class="hero__content">
            <p class="pill" aria-label="校园租赁 tagline">
              <span>UniRent 校园租赁</span>
              <span class="badge">Beta</span>
            </p>
            <h1>
              智能匹配·安全可信，
              <span class="text-gradient">校园物品租赁</span> 一站搞定
            </h1>
            <p class="lead">
              面向大学生的轻量租赁平台，覆盖图书、电子设备、运动器材、生活用品等 30+ 类目，
              让闲置流转更高效、租借更安心。
            </p>
            <div class="hero__actions">
              <button class="btn btn-primary">立即开始</button>
              <button class="btn btn-ghost">查看热租榜单</button>
            </div>
            <div class="hero__stats">
              <div v-for="stat in stats" :key="stat.label" class="stat-card">
                <div class="stat-value">{{ stat.value }}</div>
                <div class="stat-label">{{ stat.label }}</div>
              </div>
            </div>
          </div>
          <div class="hero__visual">
            <div class="floating-card">
              <div class="floating-card__header">
                <div class="avatar">UR</div>
                <div>
                  <p class="muted">校园信用值</p>
                  <p class="score">96 / 100</p>
                </div>
                <span class="badge">实名认证</span>
              </div>
              <div class="floating-card__body">
                <div class="chip-row">
                  <span class="tag" v-for="tag in tags" :key="tag">{{ tag }}</span>
                </div>
                <div class="timeline">
                  <div class="timeline__item" v-for="item in timeline" :key="item.title">
                    <div class="timeline__dot"></div>
                    <div>
                      <p class="timeline__title">{{ item.title }}</p>
                      <p class="muted">{{ item.desc }}</p>
                    </div>
                    <span class="badge" :style="{ background: item.badgeBg, color: item.badgeColor }">
                      {{ item.badge }}
                    </span>
                  </div>
                </div>
              </div>
            </div>
          </div>
        </header>
      </section>

      <div class="section-divider"></div>

      <section class="section">
        <div class="section-title">
          <span class="pill">精选类目</span>
          <h2>学生常用租赁场景</h2>
        </div>
        <p class="section-subtitle">基于校内数据，优先推荐高频且易损保障完善的物品。</p>
        <div class="grid categories">
          <article v-for="category in categories" :key="category.title" class="card category">
            <div class="category__icon" :style="{ background: category.bg }">
              {{ category.icon }}
            </div>
            <div>
              <h3>{{ category.title }}</h3>
              <p class="muted">{{ category.desc }}</p>
            </div>
            <div class="chip-row">
              <span class="tag" v-for="label in category.labels" :key="label">{{ label }}</span>
            </div>
          </article>
        </div>
      </section>

      <div class="section-divider"></div>

      <section class="section">
        <div class="section-title">
          <span class="pill">热租推荐</span>
          <h2>当前周边校区正在租的物品</h2>
        </div>
        <p class="section-subtitle">同城配送或线下自取，支持押金代管与租前验收。</p>
        <div class="grid featured">
          <article v-for="item in featured" :key="item.name" class="card featured-card">
            <div class="featured__header">
              <div class="img" :style="{ background: item.tint }">
                <span class="emoji">{{ item.emoji }}</span>
              </div>
              <div>
                <p class="badge">{{ item.tag }}</p>
                <h3>{{ item.name }}</h3>
                <p class="muted">{{ item.desc }}</p>
              </div>
              <div class="price">¥{{ item.price }} / 天</div>
            </div>
            <div class="chip-row">
              <span class="tag" v-for="spec in item.specs" :key="spec">{{ spec }}</span>
            </div>
            <div class="featured__footer">
              <div class="rating">⭐ {{ item.rating }} ({{ item.count }}人评价)</div>
              <button class="btn btn-primary">预约</button>
            </div>
          </article>
        </div>
      </section>

      <div class="section-divider"></div>

      <section class="section">
        <div class="section-title">
          <span class="pill">使用流程</span>
          <h2>3 步完成租借</h2>
        </div>
        <div class="grid process">
          <div v-for="step in steps" :key="step.title" class="card process-card">
            <div class="step-index">{{ step.index }}</div>
            <h3>{{ step.title }}</h3>
            <p class="muted">{{ step.desc }}</p>
            <div class="chip-row">
              <span class="tag" v-for="tip in step.tips" :key="tip">{{ tip }}</span>
            </div>
          </div>
        </div>
      </section>
    </div>
  </main>
</template>

<script setup>
const stats = [
  { label: '累计成交', value: '128,430+' },
  { label: '平均响应', value: '3 分钟内' },
  { label: '赔付保障', value: '¥ 3000 封顶' },
];

const tags = ['校园认证', '押金托管', '信用担保', '极速响应'];

const timeline = [
  {
    title: '预约申请已通过',
    desc: '出租人将于今日 18:00 前联系确认交付方式',
    badge: '进行中',
    badgeBg: 'rgba(14, 165, 233, 0.15)',
    badgeColor: '#0369a1',
  },
  {
    title: '押金托管到账',
    desc: '资金由平台冻结，签收后自动释放',
    badge: '安全',
    badgeBg: 'rgba(34, 197, 94, 0.14)',
    badgeColor: '#15803d',
  },
];

const categories = [
  {
    icon: '💻',
    title: '数码/电子',
    desc: '笔记本、平板、摄影摄像、投影设备等校内赛事常用物资。',
    labels: ['高保额', '送充电器', '含配件'],
    bg: 'linear-gradient(135deg, #e0f2fe, #dfe7ff)',
  },
  {
    icon: '📚',
    title: '教材/书籍',
    desc: '教辅资料、考研书、专业参考书按周租借，随时续租。',
    labels: ['近三版', '包邮到寝', '附思维导图'],
    bg: 'linear-gradient(135deg, #f1f5f9, #e2f1ff)',
  },
  {
    icon: '🎿',
    title: '运动/出行',
    desc: '轮滑、羽毛球拍、露营帐篷、行李箱，活动周必备。',
    labels: ['消毒清洁', '损坏补贴', '跨校配送'],
    bg: 'linear-gradient(135deg, #ecfdf3, #e0f2fe)',
  },
  {
    icon: '🛋️',
    title: '生活用品',
    desc: '打印机、收纳柜、蒸锅、考试神器电子表等，短期租更划算。',
    labels: ['七天免租试用', '上门安装', '同城急速达'],
    bg: 'linear-gradient(135deg, #fff7ed, #e0f2fe)',
  },
];

const featured = [
  {
    name: 'MacBook Air M2 16G/512G',
    desc: '附赠电源 + 鼠标，适配 PS/PR、CAD 课程实训。',
    tag: '高端设备',
    price: 38,
    rating: 4.9,
    count: 892,
    emoji: '💡',
    tint: 'linear-gradient(145deg, #e0e7ff, #ecfeff)',
    specs: ['押金托管', '延误免租', '含防护壳'],
  },
  {
    name: '佳能 EOS R50 + 双镜头',
    desc: '活动采访/毕业照专用，送 128G 存储卡与三脚架。',
    tag: '摄影摄像',
    price: 52,
    rating: 4.8,
    count: 421,
    emoji: '📷',
    tint: 'linear-gradient(145deg, #fef9c3, #e0f2fe)',
    specs: ['上门培训', '意外险', '48h 免赔'],
  },
  {
    name: '高山防水帐篷 2-3 人',
    desc: '含防潮垫、露营灯、便携炉，可选保洁服务。',
    tag: '校园活动',
    price: 26,
    rating: 4.7,
    count: 305,
    emoji: '⛺',
    tint: 'linear-gradient(145deg, #dcfce7, #e0f2fe)',
    specs: ['含消毒', '自提立减', '7*24 客服'],
  },
];

const steps = [
  {
    index: '01',
    title: '浏览并提交预约',
    desc: '筛选校区、时间与押金方式，选择支持的配送/自取方式即可下单。',
    tips: ['校区过滤', '同寝送达', '押金托管'],
  },
  {
    index: '02',
    title: '完成身份与信用校验',
    desc: '学生认证 + 失物追踪协议，重要物品需刷脸双重验证。',
    tips: ['学信网认证', '信用分', '协议签署'],
  },
  {
    index: '03',
    title: '交付验收并开始计费',
    desc: '交付时核对物品状态，平台见证并出具验收单，租期结束自动结算。',
    tips: ['AI 质检', '存证凭证', '一键续租'],
  },
];
</script>

<style scoped>
.hero {
  display: grid;
  grid-template-columns: 1.2fr 1fr;
  gap: 32px;
  align-items: center;
}

.hero__content h1 {
  margin: 10px 0;
  font-size: clamp(32px, 4vw, 44px);
  line-height: 1.25;
}

.hero__content .lead {
  color: #475569;
  margin: 0 0 20px;
  max-width: 640px;
}

.text-gradient {
  background: linear-gradient(135deg, #4f46e5, #06b6d4);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
}

.hero__actions {
  display: flex;
  gap: 12px;
  margin-bottom: 24px;
}

.hero__stats {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(160px, 1fr));
  gap: 12px;
}

.stat-value {
  font-size: 24px;
  font-weight: 800;
  color: #111827;
}

.stat-label {
  color: #475569;
  font-weight: 600;
}

.hero__visual {
  position: relative;
  display: flex;
  justify-content: center;
}

.floating-card {
  width: 100%;
  max-width: 420px;
  border-radius: 22px;
  background: rgba(255, 255, 255, 0.9);
  border: 1px solid var(--border);
  box-shadow: 0 25px 45px rgba(15, 23, 42, 0.1);
  overflow: hidden;
}

.floating-card__header {
  display: flex;
  align-items: center;
  gap: 12px;
  padding: 18px;
  background: linear-gradient(135deg, rgba(91, 123, 255, 0.12), rgba(14, 165, 233, 0.1));
}

.avatar {
  width: 46px;
  height: 46px;
  border-radius: 14px;
  background: linear-gradient(145deg, #5b7bff, #0ea5e9);
  display: grid;
  place-items: center;
  color: white;
  font-weight: 800;
  letter-spacing: 1px;
}

.floating-card__body {
  padding: 16px 18px 20px;
  display: grid;
  gap: 16px;
}

.timeline {
  display: grid;
  gap: 12px;
}

.timeline__item {
  display: grid;
  grid-template-columns: auto 1fr auto;
  align-items: center;
  gap: 12px;
  padding: 12px;
  border-radius: 14px;
  border: 1px dashed var(--border);
}

.timeline__dot {
  width: 10px;
  height: 10px;
  border-radius: 50%;
  background: linear-gradient(135deg, #5b7bff, #0ea5e9);
  box-shadow: 0 0 0 6px rgba(14, 165, 233, 0.1);
}

.timeline__title {
  margin: 0;
  font-weight: 700;
  color: #0f172a;
}

.muted {
  color: #94a3b8;
  margin: 4px 0 0;
}

.categories {
  grid-template-columns: repeat(auto-fit, minmax(240px, 1fr));
}

.category {
  display: grid;
  gap: 10px;
  align-content: start;
}

.category__icon {
  width: 56px;
  height: 56px;
  border-radius: 16px;
  display: grid;
  place-items: center;
  font-size: 26px;
}

.featured {
  grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
}

.featured-card {
  display: grid;
  gap: 12px;
}

.featured__header {
  display: grid;
  grid-template-columns: auto 1fr auto;
  gap: 12px;
  align-items: center;
}

.img {
  width: 68px;
  height: 68px;
  border-radius: 18px;
  display: grid;
  place-items: center;
  box-shadow: inset 0 1px 0 rgba(255, 255, 255, 0.5), 0 10px 20px rgba(15, 23, 42, 0.08);
}

.img .emoji {
  font-size: 28px;
}

.price {
  font-weight: 800;
  color: #0f172a;
}

.featured__footer {
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.rating {
  color: #0f172a;
  font-weight: 700;
}

.process {
  grid-template-columns: repeat(auto-fit, minmax(260px, 1fr));
}

.process-card {
  display: grid;
  gap: 8px;
}

.step-index {
  width: 48px;
  height: 48px;
  border-radius: 14px;
  display: grid;
  place-items: center;
  background: linear-gradient(145deg, rgba(91, 123, 255, 0.16), rgba(14, 165, 233, 0.12));
  color: #1d4ed8;
  font-weight: 800;
}

@media (max-width: 1024px) {
  .hero {
    grid-template-columns: 1fr;
  }
  .hero__visual {
    order: -1;
  }
}

@media (max-width: 640px) {
  .hero__actions {
    flex-direction: column;
  }
  .featured__header {
    grid-template-columns: 1fr;
  }
  .featured__footer {
    flex-direction: column;
    align-items: flex-start;
    gap: 10px;
  }
}
</style>
