# Một Chatbot dựa trên MCP

(English | [中文](README_zh.md) | [日本語](README_ja.md) | [Tiếng Việt](README_vi.md)))

## Giới thiệu

👉 [Human: Give AI a camera vs AI: Instantly finds out the owner hasn't washed hair for three days【bilibili】](https://www.bilibili.com/video/BV1bpjgzKEhd/)

👉 [Handcraft your AI girlfriend, beginner's guide【bilibili】](https://www.bilibili.com/video/BV1XnmFYLEJN/)

Là một mục tương tác bằng giọng nói, chatbot XiaoZhi AI tận dụng khả năng AI của các mô hình lớn như Qwen / DeepSeek và đạt được điều khiển đa thiết bị đầu cuối thông qua giao thức MCP.

<img src="docs/mcp-based-graph.jpg" alt="Control everything via MCP" width="320">

## Ghi chú phiên bản

Phiên bản v2 hiện tại không tương thích với bảng phân vùng v1, vì vậy không thể nâng cấp từ v1 lên v2 thông qua OTA. Để biết chi tiết về bảng phân vùng, hãy xem [partitions/v2/README.md](partitions/v2/README.md).

Tất cả phần cứng chạy v1 có thể được nâng cấp lên v2 bằng cách nhấp nháy chương trình cơ sở theo cách thủ công.
Phiên bản ổn định của v1 là 1.9.2. Bạn có thể chuyển sang v1 bằng cách chạy `git checkout v1`. Chi nhánh v1 sẽ được duy trì cho đến tháng 2 năm 2026.

### Các tính năng được triển khai

- Wi-Fi / ML307 Cat.1 4G
- Đánh thức giọng nói ngoại tuyến [ESP-SR](https://github.com/espressif/esp-sr)
- Hỗ trợ hai giao thức truyền thông([Websocket](docs/websocket.md) or MQTT+UDP)
- Sử dụng codec âm thanh OPUS
- Tương tác giọng nói dựa trên kiến trúc phát trực tuyến ASR + LLM + TTS
- Nhận dạng người nói, xác định người nói hiện tại [3D Speaker](https://github.com/modelscope/3D-Speaker)
- Màn hình OLED / LCD, hỗ trợ hiển thị biểu tượng cảm xúc
- Màn hình pin và quản lý năng lượng
- Hỗ trợ đa ngôn ngữ (tiếng Trung, tiếng Anh, tiếng Nhật, tiếng Việt,...)
- Hỗ trợ nền tảng chip ESP32-C3, ESP32-S3, ESP32-P4
- MCP phía thiết bị để điều khiển thiết bị (Loa, LED, Servo, GPIO, v.v.)
- MCP phía đám mây để mở rộng khả năng mô hình lớn (điều khiển nhà thông minh, vận hành máy tính để bàn, tìm kiếm kiến thức, email, v.v.)
- Các từ đánh thức, phông chữ, biểu tượng cảm xúc và hình nền trò chuyện có thể tùy chỉnh với chỉnh sửa trực tuyến dựa trên web ([Custom Assets Generator](https://github.com/78/xiaozhi-assets-generator))

## Phần cứng

### Thực hành tự làm Breadboard

Xem hướng dẫn tài liệu Feishu:
👉 ["XiaoZhi AI Chatbot Encyclopedia"](https://ccnphfhqs21z.feishu.cn/wiki/F5krwD16viZoF0kKkvDcrZNYnhb?from=from_copylink)

Bản trình diễn Breadboard:

![Breadboard Demo](docs/v1/wiring2.jpg)

### Hỗ trợ hơn 70 phần cứng nguồn mở (Danh sách một phần)

- <a href="https://oshwhub.com/li-chuang-kai-fa-ban/li-chuang-shi-zhan-pai-esp32-s3-kai-fa-ban" target="_blank" title="LiChuang ESP32-S3 Development Board">LiChuang ESP32-S3 Development Board</a>
- <a href="https://github.com/espressif/esp-box" target="_blank" title="Espressif ESP32-S3-BOX3">Espressif ESP32-S3-BOX3</a>
- <a href="https://docs.m5stack.com/zh_CN/core/CoreS3" target="_blank" title="M5Stack CoreS3">M5Stack CoreS3</a>
- <a href="https://docs.m5stack.com/en/atom/Atomic%20Echo%20Base" target="_blank" title="AtomS3R + Echo Base">M5Stack AtomS3R + Echo Base</a>
- <a href="https://gf.bilibili.com/item/detail/1108782064" target="_blank" title="Magic Button 2.4">Magic Button 2.4</a>
- <a href="https://www.waveshare.net/shop/ESP32-S3-Touch-AMOLED-1.8.htm" target="_blank" title="Waveshare ESP32-S3-Touch-AMOLED-1.8">Waveshare ESP32-S3-Touch-AMOLED-1.8</a>
- <a href="https://github.com/Xinyuan-LilyGO/T-Circle-S3" target="_blank" title="LILYGO T-Circle-S3">LILYGO T-Circle-S3</a>
- <a href="https://oshwhub.com/tenclass01/xmini_c3" target="_blank" title="XiaGe Mini C3">XiaGe Mini C3</a>
- <a href="https://oshwhub.com/movecall/cuican-ai-pendant-lights-up-y" target="_blank" title="Movecall CuiCan ESP32S3">CuiCan AI Pendant</a>
- <a href="https://github.com/WMnologo/xingzhi-ai" target="_blank" title="WMnologo-Xingzhi-1.54">WMnologo-Xingzhi-1.54TFT</a>
- <a href="https://www.seeedstudio.com/SenseCAP-Watcher-W1-A-p-5979.html" target="_blank" title="SenseCAP Watcher">SenseCAP Watcher</a>
- <a href="https://www.bilibili.com/video/BV1BHJtz6E2S/" target="_blank" title="ESP-HI Low Cost Robot Dog">ESP-HI Low Cost Robot Dog</a>

<div style="display: flex; justify-content: space-between;">
  <a href="docs/v1/lichuang-s3.jpg" target="_blank" title="LiChuang ESP32-S3 Development Board">
    <img src="docs/v1/lichuang-s3.jpg" width="240" />
  </a>
  <a href="docs/v1/espbox3.jpg" target="_blank" title="Espressif ESP32-S3-BOX3">
    <img src="docs/v1/espbox3.jpg" width="240" />
  </a>
  <a href="docs/v1/m5cores3.jpg" target="_blank" title="M5Stack CoreS3">
    <img src="docs/v1/m5cores3.jpg" width="240" />
  </a>
  <a href="docs/v1/atoms3r.jpg" target="_blank" title="AtomS3R + Echo Base">
    <img src="docs/v1/atoms3r.jpg" width="240" />
  </a>
  <a href="docs/v1/magiclick.jpg" target="_blank" title="Magic Button 2.4">
    <img src="docs/v1/magiclick.jpg" width="240" />
  </a>
  <a href="docs/v1/waveshare.jpg" target="_blank" title="Waveshare ESP32-S3-Touch-AMOLED-1.8">
    <img src="docs/v1/waveshare.jpg" width="240" />
  </a>
  <a href="docs/v1/lilygo-t-circle-s3.jpg" target="_blank" title="LILYGO T-Circle-S3">
    <img src="docs/v1/lilygo-t-circle-s3.jpg" width="240" />
  </a>
  <a href="docs/v1/xmini-c3.jpg" target="_blank" title="XiaGe Mini C3">
    <img src="docs/v1/xmini-c3.jpg" width="240" />
  </a>
  <a href="docs/v1/movecall-cuican-esp32s3.jpg" target="_blank" title="CuiCan">
    <img src="docs/v1/movecall-cuican-esp32s3.jpg" width="240" />
  </a>
  <a href="docs/v1/wmnologo_xingzhi_1.54.jpg" target="_blank" title="WMnologo-Xingzhi-1.54">
    <img src="docs/v1/wmnologo_xingzhi_1.54.jpg" width="240" />
  </a>
  <a href="docs/v1/sensecap_watcher.jpg" target="_blank" title="SenseCAP Watcher">
    <img src="docs/v1/sensecap_watcher.jpg" width="240" />
  </a>
  <a href="docs/v1/esp-hi.jpg" target="_blank" title="ESP-HI Low Cost Robot Dog">
    <img src="docs/v1/esp-hi.jpg" width="240" />
  </a>
</div>

## Phần mềm

### Nạp chương trình

Đối với người mới bắt đầu, nên sử dụng chương trình cơ sở có thể được flash mà không cần thiết lập môi trường phát triển.

The firmware connects to the official [xiaozhi.me](https://xiaozhi.me) server by default. Personal users can register an account to use the Qwen real-time model for free.

👉 [Beginner's Firmware Flashing Guide](https://ccnphfhqs21z.feishu.cn/wiki/Zpz4wXBtdimBrLk25WdcXzxcnNS)

### Môi trường phát triển

- Cursor or VSCode
- Cài đặt plugin ESP-IDF, chọn SDK phiên bản 5.4 trở lên
- Linux tốt hơn Windows để biên dịch nhanh hơn và ít sự cố trình điều khiển hơn
- Dự án này sử dụng kiểu mã Google C++, vui lòng đảm bảo tuân thủ khi gửi mã
### Tài liệu dành cho nhà phát triển

- [Custom Board Guide](docs/custom-board.md) - Tìm hiểu cách tạo bo mạch tùy chỉnh cho XiaoZhi AI
- [MCP Protocol IoT Control Usage](docs/mcp-usage.md) - Tìm hiểu cách điều khiển các thiết bị IoT thông qua giao thức MCP
- [MCP Protocol Interaction Flow](docs/mcp-protocol.md) - Triển khai giao thức MCP phía thiết bị
- [MQTT + UDP Hybrid Communication Protocol Document](docs/mqtt-udp.md)
- [A detailed WebSocket communication protocol document](docs/websocket.md)

## Cấu hình mô hình lớn

Nếu bạn đã có thiết bị chatbot XiaoZhi AI và đã kết nối với máy chủ chính thức, bạn có thể đăng nhập vào [xiaozhi.me](https://xiaozhi.me) Bảng điều khiển để cấu hình.

👉 [Backend Operation Video Tutorial (Old Interface)](https://www.bilibili.com/video/BV1jUCUY2EKM/)

## Các dự án mã nguồn mở liên quan

Để triển khai máy chủ trên máy tính cá nhân, hãy tham khảo các dự án mã nguồn mở sau:
- [xinnan-tech/xiaozhi-esp32-server](https://github.com/xinnan-tech/xiaozhi-esp32-server) Python server
- [joey-zhou/xiaozhi-esp32-server-java](https://github.com/joey-zhou/xiaozhi-esp32-server-java) Java server
- [AnimeAIChat/xiaozhi-server-go](https://github.com/AnimeAIChat/xiaozhi-server-go) Golang server
- [hackers365/xiaozhi-esp32-server-golang](https://github.com/hackers365/xiaozhi-esp32-server-golang) Golang server

Các dự án khách hàng khác sử dụng giao thức truyền thông XiaoZhi:
- [huangjunsen0406/py-xiaozhi](https://github.com/huangjunsen0406/py-xiaozhi) Python client
- [TOM88812/xiaozhi-android-client](https://github.com/TOM88812/xiaozhi-android-client) Android client
- [100askTeam/xiaozhi-linux](http://github.com/100askTeam/xiaozhi-linux) Linux client by 100ask
- [78/xiaozhi-sf32](https://github.com/78/xiaozhi-sf32) Bluetooth chip firmware by Sichuan
- [QuecPython/solution-xiaozhiAI](https://github.com/QuecPython/solution-xiaozhiAI) QuecPython firmware by Quectel

Custom Assets Tools:

- [78/xiaozhi-assets-generator](https://github.com/78/xiaozhi-assets-generator) Custom Assets Generator (Wake words, fonts, emojis, backgrounds)

## Về dự án

Đây là một dự án ESP32 mã nguồn mở, được phát hành theo giấy phép MIT, cho phép bất kỳ ai sử dụng nó miễn phí, bao gồm cả cho mục đích thương mại.

Chúng tôi hy vọng dự án này sẽ giúp mọi người hiểu được sự phát triển phần cứng AI và áp dụng các mô hình ngôn ngữ lớn phát triển nhanh chóng vào các thiết bị phần cứng thực.

Nếu bạn có bất kỳ ý tưởng hoặc đề xuất nào, vui lòng nêu vấn đề hoặc tham gia [Discord](https://discord.gg/C759fGMBcZ) hoặc QQ group: 994694848

## Lịch sử phát triển

<a href="https://star-history.com/#78/xiaozhi-esp32&Date">
 <picture>
   <source media="(prefers-color-scheme: dark)" srcset="https://api.star-history.com/svg?repos=78/xiaozhi-esp32&type=Date&theme=dark" />
   <source media="(prefers-color-scheme: light)" srcset="https://api.star-history.com/svg?repos=78/xiaozhi-esp32&type=Date" />
   <img alt="Star History Chart" src="https://api.star-history.com/svg?repos=78/xiaozhi-esp32&type=Date" />
 </picture>
</a>

