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
          base: header, activity, community, repositories, metadata 
          plugin_introduction: yes
#          plugin_sponsors: yes

          plugin_isocalendar: yes  
          plugin_isocalendar_duration: full-year  

          plugin_languages: yes  
          plugin_languages_details: bytes-size, percentage  

          plugin_achievements: yes

          plugin_achievements_threshold: X  
          plugin_achievements_display: detailed  

          plugin_calendar: yes  
          plugin_calendar_limit: 11

          plugin_habits: yes  
          plugin_habits_facts: yes 
          plugin_habits_charts: yes 

          plugin_licenses: yes 
          plugin_licenses_setup: npm ci 
    
          plugin_skyline_frames: 120  
          plugin_skyline_quality: 1  

          plugin_stargazers: yes 
          plugin_stargazers_charts_type: chartist  

          plugin_support: yes  

          plugin_topics: yes  
          plugin_topics_limit: 0
          plugin_topics_mode: icons
