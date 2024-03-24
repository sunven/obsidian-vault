# temp

默认样式
- 圆角
- Modal esc close

默认校验规则
- input 50 ...

message ,notify
- 队列消费  控制连续弹出错误？

## 登录

**google**
- mongodb
- 沉浸式翻译
- clerk

**github**
- vercel

qq email
- https://discord.com/

```yaml
patch:
  style/horizontal: true
  style/color_scheme: cool_breeze
  preset_color_schemes:
    cool_breeze:
      name: 清風／Cool Breeze
      author: skoj <skoj@qq.com>
      text_color: 255
      back_color: 16776187
      border_color: 16755370
      label_color: 5616723
      hilited_text_color: 206
      hilited_back_color: 16776187
      candidate_text_color: 37120
      comment_text_color: 5616723
      hilited_candidate_text_color: 7274554
      hilited_comment_text_color: 5616723
      hilited_candidate_back_color: 16766636
      hilited_label_color: 10438496
```

```yaml
patch:
  menu/page_size: 7
  # 仅使用「雾凇拼音」的默认配置，配置此行即可
  # __include: rime_ice_suggestion:/
  # 以下根据自己所需自行定义，仅做参考。
  # 针对对应处方的定制条目，请使用 <recipe>.custom.yaml 中配置，例如 rime_ice.custom.yaml
  __patch:
    key_binder/bindings/+:
      # 开启逗号句号翻页
      - { when: paging, accept: comma, send: Page_Up }
      - { when: has_menu, accept: period, send: Page_Down }

```