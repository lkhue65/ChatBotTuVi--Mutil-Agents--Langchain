# Chatbot Xem Tử Vi - LangChain
## Giới thiệu
Chatbot xem tử vi được xây dựng bằng LangChain, kết hợp với các mô hình ngôn ngữ lớn (LLM) để cung cấp dự đoán về tử vi dựa trên ngày tháng năm sinh và giờ sinh.

## Tính Năng

- **Cung Mệnh & Tính Cách**: Cung cấp thông tin về cung mệnh dựa trên ngày sinh và phân tích tính cách.
- **Điểm Mạnh & Dự Báo Sự Nghiệp**: Dự đoán các khả năng đặc biệt, đồng thời phân tích những ngành nghề phù hợp.
- **Mối Quan Hệ**: Phân tích tính cách để xác định quan hệ đối với người xung quanh, bao gồm bạn bè, đối tác, gia đình.
- **Lời Khuyên**: Đưa ra những lời khuyên về cuộc sống, nghề nghiệp và quan hệ xã hội.

## Công nghệ sử dụng
- **LangChain**
Thư viện LangChain giúp xây dựng các ứng dụng AI sử dụng mô hình ngôn ngữ lớn (LLM).
Các module chính được sử dụng:
langchain_community.vectorstores.FAISS: Lưu trữ vector bằng FAISS để tìm kiếm nhanh.
langchain_openai.OpenAIEmbeddings: Sử dụng mô hình text-embedding-3-large của OpenAI để nhúng văn bản thành vector.
langchain_text_splitters.CharacterTextSplitter: Chia nhỏ tài liệu thành các đoạn văn bản để xử lý hiệu quả hơn.
- **FAISS (Facebook AI Similarity Search)**
Công cụ tìm kiếm vector hiệu suất cao để lưu trữ và tìm kiếm các nhúng (embeddings).
Được sử dụng để lưu trữ các embedding từ tài liệu về từ điển tử vi và tử vi hàm số để hỗ trợ truy vấn sau này.
- **OpenAI Embeddings API**
Sử dụng mô hình text-embedding-3-large để chuyển đổi văn bản thành vector số.
Những vector này sẽ được lưu vào FAISS để tìm kiếm tương tự (similarity search).
- **LangSmith:**
  LangSmith giúp theo dõi và kiểm tra quá trình xử lý trong LangChain, đảm bảo hệ thống hoạt động hiệu quả.

 ## Sơ đồ luồng:
![MutilAgentsGraph](https://github.com/user-attachments/assets/99772916-6a2a-4f40-be65-5f24c04df0e3) <br>
Dựa theo kiến trúc Agent Supervisor, trong đó, mỗi agent sẽ thực hiện phần tác vụ riêng của mình đồng thời gửi phản hồi về agent supervisor. Agent supervisor sẽ đóng vai trò giám sát kết quả đầu ra và phản hồi lại mỗi agent ( https://blog.langchain.dev/langgraph-multi-agent-workflows/).<br>

 ![Graph](https://github.com/user-attachments/assets/84da761d-d4dd-4ed5-99b7-262f7865989a)<br>
 




  
   
