# Chatbot Xem Tử Vi - LangChain
## Giới thiệu
Chatbot xem tử vi được xây dựng bằng LangChain, kết hợp với các mô hình ngôn ngữ lớn (LLM) lấy thông tin từ hai quyển sách là Tử điển tử vi và Tử vi hàm số để cung cấp dự đoán về tử vi dựa trên ngày tháng năm sinh và giờ sinh.

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
<p align="center">
  <img src="https://github.com/user-attachments/assets/84da761d-d4dd-4ed5-99b7-262f7865989a" alt="Graph">
</p>
Trong sơ đồ trên:<br>

- **document_team** chia thành **horoscope_dictionary_agent** và **mathematical_horoscope_agents**. Nhiệm vụ:
  - **horoscope_dictionary_agent**  
    - Phân tích câu hỏi để xác định thuật ngữ tử vi.  
    - Tra cứu và cung cấp định nghĩa từ từ điển tử vi.  
    - Giải thích theo ngữ cảnh mà không thực hiện tính toán.  
  - **mathematical_horoscope_agents**  
    - Xác định yếu tố liên quan đến công thức toán học trong tử vi.  
    - Truy xuất dữ liệu và cung cấp thông tin theo mô hình toán học.  
    - Đảm bảo kết quả chính xác về mặt số học.  


  - **agent_aggregation** có nhiệm vụ:
    - Tổng hợp thông tin từ các agent khác.  
    - Đánh giá tính liên quan, nhất quán và độ chính xác của dữ liệu.  
    - Cung cấp câu trả lời mạch lạc, chính xác, phù hợp với ý định của người dùng.  
  
- **agent_formatting** có nhiệm vụ::
  - Định dạng và trình bày câu trả lời sao cho rõ ràng, súc tích.
  - Đảm bảo nội dung có cấu trúc hợp lý, dễ hiểu.
  - Cung cấp đầu ra trau chuốt, sẵn sàng truyền tải ngay lập tức.

- **top_level_orchestrator_agent** đóng vai trò người giám sát có nhiệm vụ:
  = Quản lý toàn bộ hệ thống tư vấn.
  - Tiếp nhận truy vấn từ người dùng để phối hợp với document_team để lập kế hoạch truy vấn chính xác.
  - Phân bổ truy vấn đến nhóm nghiên cứu tài liệu, bao gồm horoscope_dictionary_agent và mathematical_horoscope_agents.
  - Thu thập và đánh giá phản hồi từ các agent tài liệu bằng agent_aggregation, đảm bảo kết quả tổng hợp nhất quán và phù hợp với câu hỏi của người dùng.
  - Hướng dẫn agent_formatting định dạng và trình bày câu trả lời một cách rõ ràng, mạch lạc.
  - Đảm bảo phối hợp trơn tru giữa các tác vụ, thông tin có độ chính xác cao và câu trả lời cuối cùng có tính rõ ràng, dễ hiểu.<br>
  ***Demo**: Với message input như sau: "Người có giới tính nam, sinh ngày 20/07/2002 giờ 0:30p có mệnh là gì.và đánh giá tổng quan lá số của người này.Hệ thống sẽ cho ra dự đoán như sau:
    ![image](https://github.com/user-attachments/assets/0190a44d-ea0d-470d-8cfb-9726806cd5ca)

    
  

  

 




  
   
