# Phân Tích & Dự Đoán Xu Hướng Mạng Xã Hội
**Nguồn dữ liệu:** Viral Social Media Trends & Engagement Analysis
[Nguồn dữ liệu: https://www.kaggle.com/datasets/atharvasoundankar/viral-social-media-trends-andengagement-analysis](Nguồn dữ liệu: https://www.kaggle.com/datasets/atharvasoundankar/viral-social-media-trends-andengagement-analysis)

**Tổng Quan**
Dự án này nhằm phân tích các xu hướng lan truyền trên nhiều nền tảng mạng xã hội
(TikTok, Instagram, Twitter, YouTube) thông qua các chỉ số tương tác và dự đoán xu hướng
hashtag trong tương lai. Mục tiêu là cung cấp các phân tích chuyên sâu giúp tối ưu hóa
chiến lược nội dung và marketing trên mạng xã hội.

**Mục tiêu chính:**

• Xác định các yếu tố quan trọng ảnh hưởng đến mức độ lan truyền và tương tác của
nội dung.
• So sánh mức độ tương tác giữa các nền tảng và loại nội dung khác nhau.
• Cung cấp thông tin hữu ích để tối ưu hóa chiến lược marketing trên mạng xã hội.

## **Kết quả:**

**Hiệu suất Platform:**

![image](https://github.com/user-attachments/assets/0fa8ff5c-2f39-4974-bff8-3f5ddd114e18)


**Hiệu suất Content Type:**

![image](https://github.com/user-attachments/assets/aa6c4a4e-bf5d-4143-9cff-182ec62aef13)

**Top 10 bài viết có Engagement Rate cao nhất**

![image](https://github.com/user-attachments/assets/d31a7701-2e62-40dd-96c8-7552706f15c0)

-Post và Short video là 2 định dạng chiếm đa số các bài viết có Engagement Rate cao nhất.

**Top 5 Hashtag phổ biến:**

![image](https://github.com/user-attachments/assets/a7825467-115c-4018-8390-27bd4cb73a02)


**Hiệu suất theo khu vực**

![image](https://github.com/user-attachments/assets/4fd0d199-bcc0-446b-8486-7e107d660a4d)


**Mức độ tương quan với Engagement Rate**

![image](https://github.com/user-attachments/assets/9e7b169d-b1e7-4ebe-9b73-c4292f3960f7)

Views và Engagement Rate (%): Tương quan âm mạnh (-0.70)
→ Những bài có nhiều view chưa chắc đã có tỷ lệ tương tác cao.

Likes và Engagement Rate (%): Likes có tương quan tốt với Engagement Rate (+0.43)
→ Lượt thích là chỉ số phản ánh hiệu quả tốt nhất trong tương tác.

Shares và Comments có tương quan nhẹ với Engagement Rate.
→ Không ảnh hưởng đến Engagement Rate.

## **Mô Tả Dữ Liệu**
**Tập Dữ Liệu:** Viral_Social_Media_Trends.csv
Tập dữ liệu này gồm 5.000 bài đăng viral trên mạng xã hội với các đặc điểm sau:

    • Post_ID: Mã định danh duy nhất của bài đăng.
    • Platform: Nền tảng mạng xã hội (TikTok, Instagram, Twitter, YouTube).
    • Hashtag: Hashtag đang thịnh hành gắn với bài đăng.
    • Content_Type: Loại nội dung (Reel, Video, Post, Shorts, Tweet, v.v.).
    • Region: Quốc gia nơi bài đăng đạt được sức hút lớn.
    • Views: Tổng số lượt xem.
    • Likes: Số lượt thích.
    • Shares: Số lần chia sẻ.
    • Comments: Số bình luận.
    • Engagement_Level: Mức độ tương tác (Thấp, Trung bình, Cao).
    
