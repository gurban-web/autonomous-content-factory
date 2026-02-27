# Otonom Social Media Content Factory

Antigravity + Pinokio + AI Studio + n8n pipeline sistemi.

## 1. Arxitektura Strukturası
- **Antigravity (IDE/Beyin):** Əsas kod bazası, multi-agent orkestrasiya və proyekt idarəetməsi.
- **Google AI Studio (Design Lab):** Prompt dizaynı, JSON şemaların optimizasiyası və rapid prototyping.
- **Pinokio (Local Orchestration):** Lokal modellər (LLM, Vision), UI avtomatlaşdırma (Social Media upload) və sistem boot scriptləri.
- **n8n (Distribution):** Avtomatik paylaşım və scheduler qatı.

## 2. Google AI Studio – Prompt & Schema Design
### Video Script Generator (JSON Mode)
**System Prompt:**
`Sən peşəkar bir SMM eksperti və video script yazarsan. Verilən newsletter-i analiz edib, TikTok/Reels üçün 15-30 saniyəlik dinamik video scripti çıxarmalısan.`

**JSON Schema:**
```json
{
  "project_id": "string",
  "scenes": [
    {
      "time": "string",
      "visual": "string (b-roll description)",
      "audio": "string (narration text)",
      "overlay": "string (on-screen text)"
    }
  ],
  "music_mood": "string",
  "cta": "string"
}
```

## 3. Pinokio – Automations
### Factory Starter Script (`factory_start.json`)
Bu script 3 terminalı, n8n-i və preview browserini 1 kliklə ayağa qaldırır:
```json
{
  "run": [
    { "method": "shell.run", "params": { "message": "npm run dev", "on": "dashboard" } },
    { "method": "shell.run", "params": { "message": "npx tsx src/index.ts", "on": "claw-bot" } },
    { "method": "shell.run", "params": { "message": "npx n8n start", "on": "n8n" } },
    { "method": "browser.open", "params": { "url": "http://localhost:3000/dashboard" } }
  ]
}
```

## 4. Maliyyət və Resurs Optimizasiyası
- **Disk Space:** Ollama (70GB+ modeller) silindi. Yalnız lazımi kiçik modellər və API-lər (Gemini Flash) istifadə olunur.
- **API Cost:** Gemini Flash Lite ilə 1M token ~0.20$. Lokal orkestrasiya ilə aylıq xərc minimumda saxlanılır.


## 5. Antigravity Super Skills (Agentic Workflows)
Antigravity-nin agentic sistemini aşağıdakı "super skiller" ilə gücləndiririk:

### A. Trend Analyzer Agent
- **Görəvi:** Sosial media trendlərini (TikTok Creative Center, Google Trends) skan edir.
- **Skill:** Newsletter-i sadəcə "text" olaraq deyil, həmin an viral olan "hook" strukturları ilə birləşdirir.
- **Antigravity Rule:** `IF trend_score > 0.8 THEN use_viral_hook_template`.

### B. Brand Consistency & QA Agent
- **Görəvi:** Render olunmazdan əvvəl bütün assetləri (image, text, audio) yoxlayır.
- **Skill:** Rəng tonları, fontlar və loqo yerləşimi markaya uyğundurmu? (Vision model inteqrasiyası ilə).
- **Antigravity Rule:** `REJECT IF logo_not_visible OR font_family != 'Montserrat'`.

### C. Auto-Optimizer Agent (Coding Skill)
- **Görəvi:** Remotion kodunu analiz edir.
- **Skill:** Render vaxtını azaltmaq üçün ağır animasiyaları sadələşdirir və ya assetləri (image compression) avtomatik optimizasiya edir.
- **Antigravity Workflow:** `on_render_failure -> analyze_code -> simplify_layers -> retry`.

### D. Revenue Strategist Agent
- **Görəvi:** Abacus Dashboard-dan gələn datanı (view count, CTR) analiz edir.
- **Skill:** Hansı tip kontentin daha çox pul qazandırdığını tapır və növbəti batch-i həmin "niche" üzrə planlayır.
- **Antigravity Rule:** `SET priority = high FOR niche:finance IF rpm > 5.0`.
