name: Metrics
on:
  # Schedule daily updates
  schedule: [{cron: "0 0 * * *"}]
  workflow_dispatch:
  # (optional) Run workflow when pushing on master/main
  push: {branches: ["master", "main"]}
jobs:
  github-metrics:
    runs-on: ubuntu-latest
    steps:
      - uses: lowlighter/metrics@latest
        with:
          token: ${{ secrets.METRICS_TOKEN }}
          user: BEPb
          config_timezone: Europe/Minsk
#          config_display: columns  # отображать информацию по колонкам
          committer_message: "chore: update metrics"
          template: classic
          base: header, activity, community, repositories, metadata  # базовый контент (информация о пользователе)
          plugin_introduction: yes  # общая информация о аккаунте
#          plugin_sponsors: yes

          plugin_isocalendar: yes  # 3д изокалендарь
          plugin_isocalendar_duration: full-year  # отображает активность за полный год

          plugin_languages: yes  # отображение применяемых языков программирования
          plugin_languages_details: bytes-size, percentage  # дополнительная информация о коде размер и процент

          plugin_achievements: yes

          plugin_achievements_threshold: X  # (покажет фишки достижений которые еще не разблокированы)
          plugin_achievements_display: detailed  # детальное описание фишек достижений

          plugin_calendar: yes  # отображает активность по годам от текущего и далее
          plugin_calendar_limit: 11 # отображает активность за столько лет

          plugin_habits: yes  # активность за сутки и неделю
          plugin_habits_facts: yes  # отображает анализ вашей активность за неделю
          plugin_habits_charts: yes  # отображает характеристики

          plugin_licenses: yes  # информация о лицензиях
          plugin_licenses_setup: npm ci  # подробная информация о применяемых лицензиях

          plugin_skyline: yes  # плагин 3д активности скайлайн
          plugin_skyline_year: 2022 # за какой год
          plugin_skyline_frames: 120  # количество кадров
          plugin_skyline_quality: 1  # качество 1 - лучшее

          plugin_stargazers: yes  # активность за месяц
          plugin_stargazers_charts_type: chartist  # тип активности - плавные линии

          plugin_support: yes  # плагин поддержки

          plugin_topics: yes  # плагин ипсользуемых тем
          plugin_topics_limit: 0
          plugin_topics_mode: icons
