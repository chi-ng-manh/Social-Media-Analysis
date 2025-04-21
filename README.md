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
    
## Data processing and analysis
Using Google Colab to read and process data

**Import Library**

    import pandas as pd
    import seaborn as sns
    import matplotlib.pyplot as plt
    
**Read Data**

    df = pd.read_csv("/content/Viral_Social_Media_Trends.csv")
    df.sample(5)
    df.info()

**Create Engament Rate (%) Column**

    # Tạo cột Engagement_Rate by View, làm tròn 2 chữ số
    df['Engagement_Rate(%)'] = (((df['Likes'] + df['Shares'] + df['Comments']) / df['Views'])* 100).round(2).astype(float)
    
### **Fill Missing Value & Remove Outliner Value**

    #Fill missing Value
    df.fillna(0, inplace=True)
    
    #Remove Outliner from Engagement_Rate(%)
    Q1 = df['Engagement_Rate(%)'].quantile(0.25)
    Q3 = df['Engagement_Rate(%)'].quantile(0.75)
    IQR = Q3 - Q1
    
    # Giữ lại những giá trị nằm trong khoảng Q1 - 1.5*IQR đến Q3 + 1.5*IQR
    df_cleaned = df[(df['Engagement_Rate(%)'] >= Q1 - 1.5 * IQR) &
                            (df['Engagement_Rate(%)'] <= Q3 + 1.5 * IQR)]
                            
    df_cleaned.sample(10)
    
### **Convert Column Type**
    
    # Check Column type
    df_cleaned.info()
    
    #Check column name has any space
    print(df_cleaned.columns.tolist())
    
    #Remove space between column name
    df_cleaned.columns = df_cleaned.columns.str.strip()
    
    df_cleaned.convert_dtypes().info()
    
     #Change List Column to Catagory
    List_categorical_column = ['Platform', 'Hashtag', 'Content_Type', 'Region', 'Engagement_Level']
    df_cleaned[List_categorical_column] = df_cleaned[List_categorical_column].astype('category')
    
     # Change Post_ID column to int
     df_cleaned['Post_ID'] = df_cleaned['Post_ID'].str.replace('Post_', '').astype(int)
     
     #Cột Engagement_Rate(%) thành Float
    df_cleaned['Engagement_Rate(%)'] = df_cleaned['Engagement_Rate(%)'].astype(float)

    #check column type again
    df_cleaned.info()
    
    #loại bỏ Engagement_Level Column
    df_cleaned.drop(columns=['Engagement_Level'], inplace=True)
    df_cleaned.sample(5)
    
    # Tổng lượt bài đăng của từng nền tảng
    platform_counts = df_cleaned['Platform'].value_counts()
    print(platform_counts)
    
### **Export cleaned Date to CSV**
    # Count total post of each platform
    platform_counts = df_cleaned['Platform'].value_counts()
    print(platform_counts)
    
    # Summary according to Youtube
    df_youtube = df_cleaned[df['Platform'] == 'YouTube'].reset_index(drop=True)
    # Summary according to Twitter
    df_Twitter = df_cleaned[df['Platform'] == 'Twitter'].reset_index(drop=True)
    # Summary according to Tiktok
    df_tiktok = df_cleaned[df['Platform'] == 'TikTok'].reset_index(drop=True)
    # Summary according to Instagram
    df_instagram = df_cleaned[df['Platform'] == 'Instagram'].reset_index(drop=True)
    
    # Export cleaned data to Excel for Power BI
    with pd.ExcelWriter("Cleaned_Viral_Social_Media_Analysis.xlsx") as writer:
        df_cleaned.to_excel(writer, index=False, sheet_name="All_Data")
        df_tiktok.to_excel(writer, index=False, sheet_name="TikTok")
        df_instagram.to_excel(writer, index=False, sheet_name="Instagram")
        df_youtube.to_excel(writer, index=False, sheet_name="YouTube")
        df_Twitter.to_excel(writer, index=False, sheet_name="Twitter")
        
### **Correlation with Engagement Rate**

    # Calculate correlation matrix
    correlation_matrix = df_cleaned[['Views', 'Likes', 'Shares', 'Comments', 'Engagement_Rate(%)']].corr()
    
    # Draw heatmap
    plt.figure(figsize=(8, 6))
    sns.heatmap(correlation_matrix, annot=True, cmap='coolwarm', fmt=".2f", linewidths=0.5)
    plt.title("Heatmap Tương Quan Giữa Các Chỉ Số")
    plt.tight_layout()
    plt.show()

![image](https://github.com/user-attachments/assets/7f42791e-65ac-46f4-a3b5-8c3feac41762)
