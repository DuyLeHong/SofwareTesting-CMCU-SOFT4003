# Bài tập môn Kiểm thử phần mềm - CMCU - Kỳ Xuân 2026

## Timeline 8 tuần (phân bổ theo đề cương)

Ghi chú:
- Bài tập kỹ năng được giao và nộp hàng tuần.
- Kiểm tra giữa kỳ diễn ra **tuần 4 - tuần 6**; kiểm tra cuối kỳ là bài tập lớn theo nhóm + vấn đáp cuối học phần.

| Tuần | Nội dung theo đề cương | Bài tập / Deliverables (tương ứng tài liệu bài tập) |
|---|---|---|
| 1 | Chương 1: Tổng quan kiểm thử, QA, tiêu chuẩn chất lượng | Khởi tạo repo GitHub, đọc yêu cầu chung, chọn đối tượng test. Chuẩn hóa README và cấu trúc thư mục nộp bài. |
| 2 | Chương 2: Quy trình kiểm thử, quản lý kiểm thử, vòng đời lỗi | Bài I: JUnit (StudentAnalyzer) — cài đặt, viết unit test, chạy test & chụp kết quả, hoàn thiện README. |
| 3 | Chương 2 (tiếp): phương pháp & cấp độ kiểm thử | Bài II: Cypress (Saucedemo) — cài đặt Cypress, viết các kịch bản E2E cơ bản, chạy và lưu bằng chứng (video/ảnh). |
| 4 | Chương 3: Kỹ thuật kiểm thử (hộp đen/hộp trắng/hộp xám) | Mở rộng Bài II: bổ sung test case theo kỹ thuật (biên, tương đương, đường đi). Viết checklist hoặc test case doc ngắn. |
| 5 | Chương 4: Thiết kế test case, lập kế hoạch kiểm thử | Bài III: JMeter — thiết kế test plan, chạy thử nghiệm tải, xuất báo cáo kết quả. |
| 6 | Ôn và kiểm tra giữa kỳ (tuần 4 - tuần 6) | Nộp giữa kỳ theo yêu cầu lớp. Bắt đầu bài cộng điểm V: Quản lý lỗi với GitHub Issues/Jira (tạo issue template, tạo bug/task, triage). |
| 7 | Chương 5: Bài tập vận dụng (web/mobile/CSDL & bảo mật) | Tiếp tục bài V (đóng vòng đời bug: fix → re-test → close, báo cáo số liệu). Nếu chọn nâng cao: Bài IV Appium (không bắt buộc). |
| 8 | Ôn tập, hoàn thiện bài tập lớn cuối kỳ | Tổng hợp báo cáo cuối kỳ: repo hoàn chỉnh, tài liệu, bằng chứng chạy test, báo cáo defect metrics (nếu làm bài V), chuẩn bị vấn đáp. |

## I. Bài tập thực hành kiểm thử với JUnit

### Chủ đề: Phân tích dữ liệu điểm số học sinh

### Mục tiêu học tập:

Biết cách viết hàm xử lý có điều kiện và vòng lặp.

Viết test case bằng JUnit để kiểm thử toàn diện.

Sử dụng GitHub để quản lý mã nguồn.

Biết cách tích hợp kiểm thử vào quy trình phát triển phần mềm.


### 1. Mô tả yêu cầu chức năng

```
Viết một chương trình Java có lớp StudentAnalyzer chứa phương thức:
public class StudentAnalyzer {
    /**
     * Phân tích điểm số và trả về số lượng học sinh đạt loại Giỏi.
     * @param scores danh sách điểm số từ 0 đến 10
     * @return số học sinh đạt loại Giỏi (>= 8.0)
     * - Bỏ qua điểm âm hoặc lớn hơn 10 (coi là dữ liệu sai)
```

* - Nếu danh sách rỗng, trả về 0

```
     */
    public int countExcellentStudents(List<Double> scores) {
        // TODO: Sinh viên viết mã tại đây
    }
```


```
    /**
     * Tính điểm trung bình hợp lệ (từ 0 đến 10)
     * @param scores danh sách điểm
     * @return điểm trung bình của các điểm hợp lệ
     */
    public double calculateValidAverage(List<Double> scores) {
        // TODO: Sinh viên viết mã tại đây
    }
}
```

### Yêu cầu kỹ thuật của phương thức:

Điều kiện 1: Nếu điểm nhỏ hơn 0 hoặc lớn hơn 10 thì bỏ qua (validate).

Điều kiện 2: Nếu danh sách rỗng thì trả về kết quả mặc định (0).

Vòng lặp 1: Duyệt qua danh sách điểm để lọc học sinh giỏi.

Vòng lặp 2: Duyệt qua danh sách để tính trung bình hợp lệ.


### 2. Yêu cầu kiểm thử với JUnit

Sinh viên cần viết ca kiểm thử (test case) đơn vị cho mỗi phương thức trên:

Trường hợp bình thường:

Danh sách có nhiều điểm hợp lệ và không hợp lệ.

Danh sách toàn bộ hợp lệ.

Trường hợp biên:

Danh sách trống.

Danh sách chỉ chứa giá trị 0 hoặc 10.

Trường hợp ngoại lệ:

Có điểm < 0 hoặc > 10.

✅ Gợi ý lớp test:

```
import org.junit.jupiter.api.Test;
import static org.junit.jupiter.api.Assertions.*;
import java.util.Arrays;
import java.util.Collections;
```


```
public class StudentAnalyzerTest {
```


```
    @Test
    public void testCountExcellentStudents() {
        StudentAnalyzer analyzer = new StudentAnalyzer();
        assertEquals(2, analyzer.countExcellentStudents(Arrays.asList(9.0, 8.5, 7.0, 11.0, -1.0)));
        assertEquals(0, analyzer.countExcellentStudents(Collections.emptyList()));
    }
```


```
    @Test
    public void testCalculateValidAverage() {
        StudentAnalyzer analyzer = new StudentAnalyzer();
        assertEquals(8.17, analyzer.calculateValidAverage(Arrays.asList(9.0, 8.5, 7.0, 11.0, -1.0)), 0.01);
    }
}
```


### 3. Quy trình nộp bài

#### Bước 1. Tạo GitHub Repository

```
Đặt tên repo theo định dạng: unit-test-[HọTênKhôngDấu] (ví dụ: unit-test-NguyenVanA)
```

Chia repo làm 2 thư mục:

```
src/ chứa mã nguồn Java
test/ chứa các file test JUnit
```

#### Bước 2: Tạo các Issues trên GitHub

Tạo ít nhất 4 Issues sau:

| Tên Issue | Mô tả |
| --- | --- |
| Viết hàm countExcellentStudents() | Cần xử lý kiểm tra điểm hợp lệ và đếm học sinh giỏi |
| Viết hàm calculateValidAverage() | Tính trung bình các điểm hợp lệ |
| Viết test cho 2 hàm trên | Dùng JUnit để kiểm thử đầy đủ |
| Viết tài liệu README.md | Mô tả bài toán, cách chạy chương trình, test |

#### Bước 3: Thực hiện commit gắn với issue

Khi thực hiện từng việc, sinh viên cần:

Ghi rõ commit message liên kết với issue, ví dụ:

```
feat: implement countExcellentStudents() #1
test: add unit tests for both methods #3
docs: update README with instructions #4
Cú pháp #1 sẽ tự động liên kết commit với issue số 1, và nếu dùng từ khóa như fixes #1 hoặc closes #1 sẽ tự động đóng issue khi merge vào nhánh chính.
```

#### Bước 4. Nộp bài lên LMS

```
Tạo README.md mô tả bài tập và hướng dẫn chạy test.
```

Nộp đường link GitHub repo vào hệ thống LMS (mục "Bài tập thực hành kiểm thử với JUnit").


### Tài liệu tham khảo

Hướng dẫn JUnit 5: https://junit.org/junit5/docs/current/user-guide/

Cách tạo GitHub repo: https://docs.github.com/en/get-started/quickstart/create-a-repo


# II. Bài tập thực hành kiểm thử tự động End-to-End với Cypress


## Mục tiêu

Hiểu và thực hành các kịch bản kiểm thử tự động end-to-end phổ biến bằng cách sử dụng Cypress để kiểm tra một trang web mẫu. Sinh viên sẽ thực hiện các kịch bản như kiểm tra giao diện người dùng, đăng nhập, tìm kiếm, và gửi biểu mẫu.

## Yêu cầu

Đã cài đặt Node.js (phiên bản 14 hoặc cao hơn).

Đã cài đặt Visual Studio Code hoặc một trình soạn thảo mã khác.

```
Truy cập được trang web mẫu: https://www.saucedemo.com (một trang web được thiết kế để thực hành kiểm thử tự động).
```

Cài đặt Cypress trong dự án.

## Hướng dẫn cài đặt Cypress

```bash
Tạo một thư mục dự án mới và khởi tạo npm:
mkdir cypress-exercise
cd cypress-exercise
npm init -y
```


```
Cài đặt Cypress:
npm install cypress --save-dev
```


```
Mở Cypress:
npx cypress open
Sau khi chạy lệnh này, Cypress sẽ tạo cấu trúc thư mục và các tệp mẫu trong thư mục cypress.
```

## Kịch bản kiểm thử

```
Sinh viên sẽ tạo các bài kiểm thử cho trang web https://www.saucedemo.com. Trang web này mô phỏng một cửa hàng trực tuyến với chức năng đăng nhập, danh sách sản phẩm, và giỏ hàng.
```

### Kịch bản 1: Kiểm tra đăng nhập thành công

Mục tiêu: Kiểm tra xem người dùng có thể đăng nhập thành công với thông tin hợp lệ.

Bước thực hiện:

```
Truy cập trang https://www.saucedemo.com.
Nhập tên người dùng: standard_user.
Nhập mật khẩu: secret_sauce.
```

Nhấn nút "Login".

```
Xác minh rằng trang được chuyển hướng đến trang danh sách sản phẩm (URL chứa /inventory.html).
Tệp kiểm thử: Tạo tệp cypress/e2e/login_spec.cy.js với nội dung:
describe('Login Test', () => {
  it('Should login successfully with valid credentials', () => {
    cy.visit('https://www.saucedemo.com');
    cy.get('#user-name').type('standard_user');
    cy.get('#password').type('secret_sauce');
    cy.get('#login-button').click();
    cy.url().should('include', '/inventory.html');
  });
});
```


### Kịch bản 2: Kiểm tra đăng nhập thất bại

Mục tiêu: Kiểm tra xem hệ thống hiển thị thông báo lỗi khi đăng nhập với thông tin không hợp lệ.

Bước thực hiện:

```
Truy cập trang https://www.saucedemo.com.
Nhập tên người dùng: invalid_user.
Nhập mật khẩu: wrong_password.
```

Nhấn nút "Login".

```
Xác minh rằng thông báo lỗi được hiển thị với nội dung: Username and password do not match.
Tệp kiểm thử: Thêm vào cypress/e2e/login_spec.cy.js:
it('Should show error message with invalid credentials', () => {
  cy.visit('https://www.saucedemo.com');
  cy.get('#user-name').type('invalid_user');
  cy.get('#password').type('wrong_password');
  cy.get('#login-button').click();
  cy.get('.error-message-container').should('contain', 'Username and password do not match');
});
```


### Kịch bản 3: Kiểm tra chức năng thêm sản phẩm vào giỏ hàng

Mục tiêu: Kiểm tra xem người dùng có thể thêm một sản phẩm vào giỏ hàng sau khi đăng nhập.

Bước thực hiện:

```
Đăng nhập với thông tin hợp lệ (standard_user/secret_sauce).
```

Nhấn nút "Add to cart" của sản phẩm đầu tiên trong danh sách.

```
Xác minh rằng số lượng sản phẩm trong giỏ hàng hiển thị là 1.
Tệp kiểm thử: Tạo tệp cypress/e2e/cart_spec.cy.js với nội dung:
describe('Cart Test', () => {
  beforeEach(() => {
    cy.visit('https://www.saucedemo.com');
    cy.get('#user-name').type('standard_user');
    cy.get('#password').type('secret_sauce');
    cy.get('#login-button').click();
  });
```


```
  it('Should add a product to the cart', () => {
    cy.get('.inventory_item').first().find('.btn_inventory').click();
    cy.get('.shopping_cart_badge').should('have.text', '1');
  });
});
```


### Kịch bản 4: Kiểm tra chức năng tìm kiếm sản phẩm

Mục tiêu: Kiểm tra xem bộ lọc sản phẩm hoạt động đúng khi chọn "Price (low to high)".

Bước thực hiện:

Đăng nhập với thông tin hợp lệ.

Chọn bộ lọc "Price (low to high)" từ dropdown.

Xác minh rằng sản phẩm đầu tiên trong danh sách có giá thấp nhất.

```
Tệp kiểm thử: Thêm vào cypress/e2e/cart_spec.cy.js:
it('Should sort products by price low to high', () => {
  cy.get('.product_sort_container').select('lohi');
  cy.get('.inventory_item_price').first().should('have.text', '$7.99');
});
```


## Hướng dẫn chạy kiểm thử

Mở terminal trong thư mục dự án.

```
Chạy lệnh:
npx cypress open
```


```
Trong giao diện Cypress, chọn các tệp kiểm thử (login_spec.cy.js và cart_spec.cy.js) để chạy.
```

## Bài tập yêu cầu

Thực hiện và chạy tất cả các kịch bản kiểm thử trên.

```
Thêm một kịch bản kiểm thử mới trong cart_spec.cy.js để kiểm tra chức năng xóa sản phẩm khỏi giỏ hàng:
```

Sau khi thêm sản phẩm vào giỏ hàng, nhấn nút "Remove".

```
Xác minh rằng số lượng sản phẩm trong giỏ hàng trở về 0 (hoặc không hiển thị biểu tượng giỏ hàng).
```

Viết một kịch bản kiểm thử mới để kiểm tra quy trình thanh toán:

```
Đăng nhập, thêm sản phẩm vào giỏ hàng, đi đến trang thanh toán, điền thông tin (First Name: John, Last Name: Doe, Zip Code: 12345), và nhấn "Continue".
Xác minh rằng người dùng được chuyển đến trang xác nhận thanh toán (/checkout-step-two.html).
```

Gửi kết quả chạy kiểm thử (ảnh chụp màn hình hoặc video) và mã nguồn các tệp kiểm thử.

## Tài liệu tham khảo

```
Tài liệu chính thức của Cypress: https://docs.cypress.io
Trang web mẫu: https://www.saucedemo.com
```


# III. Kiểm thử hiệu năng với JMeter

## Mục tiêu

Hiểu cách sử dụng JMeter để thực hiện kiểm thử hiệu năng.

Thiết kế kịch bản kiểm thử với các tham số khác nhau (có tính cá nhân hoá).

Phân tích kết quả kiểm thử và viết báo cáo.

## Yêu cầu

Mỗi sinh viên sẽ sử dụng JMeter để kiểm thử hiệu năng một trang web được gán dựa trên MSSV của mình.

Sinh viên cần tạo ít nhất 3 kịch bản kiểm thử (Thread Group) với các tham số khác nhau (số lượng người dùng, thời gian chạy, hành vi người dùng).

Kết quả kiểm thử phải được trình bày trong một báo cáo ngắn gọn (dạng file text hoặc markdown).

## Hướng dẫn thực hiện

### Chọn trang web để kiểm thử

Mỗi sinh viên sẽ chọn một trang web công khai từ danh sách sau dựa trên 2 chữ số cuối của MSSV:

00-19: https://www.example.com

(Links to an external site.)


20-39: https://www.wikipedia.org

(Links to an external site.)


40-59: https://vnexpress.net

(Links to an external site.)


60-79: https://www.reddit.com

(Links to an external site.)


80-99: https://github.com

(Links to an external site.)


Ví dụ: MSSV 12345678 → 2 chữ số cuối là 78 → kiểm thử trên https://www.reddit.com

(Links to an external site.)

.

### Thiết lập JMeter

Tải và cài đặt JMeter (https://jmeter.apache.org/download_jmeter.cgi

(Links to an external site.)

).

Tạo một Test Plan mới trong JMeter.

### Tạo kịch bản kiểm thử

#### Thread Group 1: Kịch bản cơ bản

Số lượng người dùng (Threads): 10 + (MSSV % 10). Ví dụ, MSSV 12345678 → 78 % 10 = 8 → 18 người dùng.

Thời gian chạy (Loop Count): 5 lần lặp.

Hành vi: Gửi yêu cầu HTTP GET đến trang chủ của website được gán.

#### Thread Group 2: Kịch bản tải nặng

Số lượng người dùng: 50 + (MSSV % 20).

Ramp-up Period: 30 giây.

Hành vi: Gửi yêu cầu HTTP GET đến trang chủ và 1 trang con bất kỳ (sinh viên tự chọn, ví dụ: trang tìm kiếm, bài viết, hoặc danh mục).

#### Thread Group 3: Kịch bản tùy chỉnh

Số lượng người dùng: 20 + (MSSV % 15).

Thời gian chạy: 60 giây.

Hành vi: Gửi yêu cầu HTTP POST (nếu website hỗ trợ, ví dụ: gửi form tìm kiếm) hoặc GET đến 2 trang con khác nhau (sinh viên tự chọn).

Thêm HTTP Request Defaults để cấu hình URL cơ sở của website.

Thêm Listeners (ví dụ: View Results Tree, Summary Report) để thu thập kết quả.

### Cá nhân hóa kịch bản

Sinh viên phải thêm một User Defined Variables trong Test Plan, với một biến có tên là StudentID và giá trị là MSSV của mình.

Sử dụng biến này trong ít nhất một yêu cầu HTTP (ví dụ: thêm tham số ?student_id=${StudentID} vào URL của một yêu cầu GET).

### Phân tích kết quả

Chạy từng Thread Group và thu thập các chỉ số: Response Time, Throughput, Error Rate.

Lưu kết quả dưới dạng file CSV hoặc screenshot của Summary Report.

### Nộp bài qua GitHub

#### Bước 1. Tạo tài khoản GitHub (nếu chưa có): Truy cập https://github.com

(Links to an external site.)

và đăng ký tài khoản.

#### Bước 2. Tạo repository

Đăng nhập vào GitHub, nhấp vào nút "New" để tạo một repository mới.

Đặt tên repository là JMeter_Assignment_[MSSV] (thay [MSSV] bằng MSSV của bạn, ví dụ: JMeter_Assignment_12345678).

Chọn chế độ Public hoặc Private (nếu Private, mời giảng viên làm collaborator bằng email hoặc username của giảng viên).

#### Bước 3. Cài đặt Git

Tải và cài đặt Git từ https://git-scm.com/downloads

(Links to an external site.)

.

```
Cấu hình Git với email và tên của bạn:
git config --global user.email "your_email@example.com" git config --global user.name "Your Name"
```

#### Bước 4. Tải bài nộp lên GitHub

Tạo một thư mục trên máy tính, ví dụ: JMeter_Assignment.

Sao chép các file cần nộp vào thư mục này:

File JMeter (.jmx).

File báo cáo readme.md.

File kết quả kiểm thử (CSV hoặc screenshot/video).

Mở terminal/command prompt trong thư mục, chạy các lệnh sau:
git init git add . git commit -m "Nộp bài tập JMeter" git branch -M main git remote add origin https://github.com/[your-username]/JMeter_Assignment_[MSSV].git git push -u origin main

Thay [your-username] và [MSSV] bằng thông tin tương ứng.

#### Bước 5. Gửi link repository

Sao chép URL của repository trên GitHub (ví dụ: https://github.com/your-username/JMeter_Assignment_12345678

(Links to an external site.)

).

Nộp link repo vào bài tập này.

Lưu ý: Đảm bảo repository chứa đầy đủ các file yêu cầu và file báo cáo theo định dạng dưới đây.

## Lưu ý chung

Đảm bảo không gửi quá nhiều yêu cầu đến website để tránh vi phạm chính sách sử dụng (rate limiting). Nếu website có giới hạn, giảm số lượng người dùng hoặc liên hệ giảng viên để được gợi ý trang web thay thế.

Mỗi sinh viên phải có kết quả khác nhau do sự khác biệt về MSSV và lựa chọn trang con.

### Lưu ý

Đảm bảo không gửi quá nhiều yêu cầu đến website để tránh vi phạm chính sách sử dụng (rate limiting). Nếu website có giới hạn, giảm số lượng người dùng hoặc liên hệ giảng viên để được gợi ý trang web thay thế.

Mỗi sinh viên phải có kết quả khác nhau do sự khác biệt về MSSV và lựa chọn trang con.


## Tệp báo cáo mẫu

### Báo cáo kiểm thử JMeter

```
# Báo cáo kiểm thử hiệu năng bằng JMeter
```


```
## Thông tin sinh viên
```


- Họ tên: [Tên sinh viên]


```
- MSSV: [MSSV]
```


```
- Website được kiểm thử: [URL website]
```


## Mô tả kịch bản kiểm thử


1. **Kịch bản 1: Cơ bản**


- Số lượng người dùng: [10 + (MSSV % 10)]


```
- Hành vi: Gửi yêu cầu GET đến [URL trang chủ]
```


```
- Loop Count: 5
```


2. **Kịch bản 2: Tải nặng**


- Số lượng người dùng: [50 + (MSSV % 20)]


```
- Ramp-up Period: 30 giây
```


```
- Hành vi: Gửi yêu cầu GET đến [URL trang chủ] và [URL trang con]
```


3. **Kịch bản 3: Tùy chỉnh**


- Số lượng người dùng: [20 + (MSSV % 15)]


- Thời gian chạy: 60 giây


```
- Hành vi: Gửi yêu cầu [GET/POST] đến [URL trang con 1] và [URL trang con 2]
```


## Kết quả kiểm thử


- **Kịch bản 1**:


- Response Time trung bình: [giá trị] ms


- Throughput: [giá trị] yêu cầu/giây


- Error Rate: [giá trị]%


- **Kịch bản 2**:


- Response Time trung bình: [giá trị] ms


- Throughput: [giá trị] yêu cầu/giây


- Error Rate: [giá trị]%


- **Kịch bản 3**:


- Response Time trung bình: [giá trị] ms


- Throughput: [giá trị] yêu cầu/giây


- Error Rate: [giá trị]%


## Nhận xét


```
- [Nhận xét về hiệu năng của website, ví dụ: thời gian phản hồi có ổn định không, có lỗi nào đáng chú ý không, website có chịu được tải không]
```


# IV. Kiểm thử tự động ứng dụng di động bằng Appium (bài đọc thêm, không bắt buộc)

#### Mục tiêu

Sinh viên sẽ sử dụng Appium để viết các kịch bản kiểm thử tự động cho một ứng dụng di động thuộc danh mục Giáo dục và Học tập (Android hoặc iOS). Mỗi sinh viên sẽ chọn một ứng dụng hoặc tính năng khác nhau dựa trên mã số sinh viên để đảm bảo tính cá nhân hóa. Bài tập yêu cầu thiết lập môi trường, viết test case, chạy kiểm thử, và báo cáo kết quả trên GitHub.

#### Yêu cầu

Cá nhân hóa bài tập:

Mỗi sinh viên sẽ chọn một ứng dụng di động miễn phí thuộc danh mục Giáo dục và Học tập từ Google Play Store (hoặc App Store nếu dùng iOS) dựa trên 2 chữ số cuối của mã số sinh viên. Ví dụ:

Nếu mã số sinh viên là 12345678, sinh viên sẽ chọn một ứng dụng thuộc danh mục con tương ứng với số 78 từ danh sách dưới đây.

Công thức: Lấy 2 chữ số cuối của mã số sinh viên, tính mod 5 để chọn danh mục con:

0: Ứng dụng học ngoại ngữ

1: Ứng dụng học toán hoặc khoa học

2: Ứng dụng học kỹ năng mềm hoặc nghề nghiệp

3: Ứng dụng học tập dành cho trẻ em

4: Ứng dụng quản lý học tập hoặc ghi chú học thuật

Sinh viên phải chọn một ứng dụng cụ thể được đánh giá được xếp hạng top 20 và ưu tiên ứng dụng có tích hợp AI tạo sinh trong danh mục con đó và không được trùng với bạn cùng lớp (đăng ký bằng cách kiểm tra

(Links to an external site.)

bạn đã đăng ký chưa, rồi khi điền vào đây

(Links to an external site.)

trước khi bắt đầu).

Nhiệm vụ:

Cài đặt môi trường: Thiết lập môi trường Appium (bao gồm Appium Server, Android SDK/iOS Simulator, và các công cụ cần thiết như Java, Node.js, v.v.).

Viết test case: Tạo ít nhất 3 test case để kiểm thử các tính năng chính của ứng dụng đã chọn. Ví dụ:

Kiểm tra đăng nhập hoặc tạo tài khoản (nếu có).

Kiểm tra một tính năng học tập chính (ví dụ: hoàn thành một bài học ngôn ngữ, giải một bài toán, tạo flashcard).

Kiểm tra một tính năng giao diện (UI) như chuyển đổi giữa các màn hình hoặc kiểm tra thông báo lỗi khi nhập sai dữ liệu.

Tự động hóa: Sử dụng Appium với ngôn ngữ lập trình Java hoặc Python để viết các kịch bản kiểm thử tự động cho các test case.

Báo cáo: Tạo một file README.md trên GitHub bao gồm:

Mô tả ứng dụng đã chọn và lý do chọn.

Danh sách các test case (mô tả ngắn gọn).

Hướng dẫn chạy kịch bản kiểm thử (các bước thiết lập môi trường và lệnh chạy).

Kết quả kiểm thử (bao gồm ảnh chụp màn hình hoặc video ngắn).

Khó khăn gặp phải và cách khắc phục.

Nộp bài: Đẩy toàn bộ mã nguồn lên GitHub và nộp link repository qua hệ thống quản lý học tập (hoặc email cho giảng viên).

Yêu cầu kỹ thuật:

Sử dụng Appium với framework kiểm thử như TestNG (Java) hoặc PyTest (Python).

Mã nguồn phải được tổ chức rõ ràng, có comment giải thích các bước.

Sử dụng Git để quản lý mã nguồn, với ít nhất 3 commit (mỗi commit mô tả rõ ràng công việc đã làm).

Đảm bảo kịch bản kiểm thử chạy được trên ít nhất một thiết bị/emulator (Android hoặc iOS).

Tiêu chí đánh giá:

Đúng yêu cầu: Chọn đúng ứng dụng theo danh mục con, viết đủ 3 test case, mã nguồn chạy được.

Chất lượng mã: Mã sạch, có comment, tổ chức tốt, sử dụng framework kiểm thử phù hợp.

Báo cáo README.md: Rõ ràng, đầy đủ thông tin, có ảnh chụp hoặc video minh họa.

#### Hướng dẫn thực hiện

Cài đặt môi trường:

Cài đặt Appium Server qua npm (npm install -g appium).

Cài đặt Android Studio (cho Android) hoặc Xcode (cho iOS).

Thiết lập biến môi trường cho Java, Android SDK, hoặc iOS Simulator.

Tải ứng dụng đã chọn (APK hoặc App Store) và lấy thông tin package/activity (dùng công cụ như apkanalyzer hoặc Appium Desktop Inspector).

Viết mã kiểm thử:

Sử dụng Appium để tương tác với ứng dụng (tìm phần tử bằng ID, XPath, hoặc Accessibility ID).

Viết các test case sử dụng framework như TestNG hoặc PyTest.

Xử lý ngoại lệ (ví dụ: khi ứng dụng crash hoặc phần tử không tìm thấy).

Tạo repository GitHub:

Tạo một repository công khai với tên rõ ràng (ví dụ: Appium_Assignment_<MSSV>).

Đẩy mã nguồn, bao gồm file kiểm thử, file cấu hình Appium, và README.md.

Commit thường xuyên với thông điệp rõ ràng.

#### Ví dụ mã kiểm thử (Python với PyTest)

Dưới đây là một ví dụ mẫu về kiểm thử một ứng dụng học ngoại ngữ (giả lập), sử dụng Python và PyTest. Sinh viên cần điều chỉnh mã này cho ứng dụng cụ thể của mình.

```
import pytest
from appium import webdriver
from appium.webdriver.common.appiumby import AppiumBy
from appium.options.android import UiAutomator2Options
import time
```


```
@pytest.fixture
def driver():
    # Cấu hình Desired Capabilities
    capabilities = UiAutomator2Options().load_capabilities({
        "platformName": "Android",
        "appium:automationName": "UiAutomator2",
```

"appium:appPackage": "com.example.languageapp",  # Thay bằng package của ứng dụng

"appium:appActivity": "com.example.languageapp.MainActivity",  # Thay bằng activity của ứng dụng

```
        "appium:deviceName": "emulator-5554",
        "appium:noReset": True
    })
    driver = webdriver.Remote("http://localhost:4723", options=capabilities)
    yield driver
    driver.quit()
```


```
def test_complete_lesson(driver):
    # Test case: Hoàn thành một bài học ngôn ngữ
    start_lesson_button = driver.find_element(AppiumBy.ID, "com.example.languageapp:id/start_lesson")
    start_lesson_button.click()
```


```
    time.sleep(2)
    answer_field = driver.find_element(AppiumBy.ID, "com.example.languageapp:id/answer_input")
    answer_field.send_keys("Hello")
```


```
    submit_button = driver.find_element(AppiumBy.ID, "com.example.languageapp:id/submit_button")
    submit_button.click()
```


```
    time.sleep(2)
    result_text = driver.find_element(AppiumBy.ID, "com.example.languageapp:id/result_text")
    assert result_text.text == "Correct!"
```


```
def test_invalid_answer(driver):
    # Test case: Nhập câu trả lời sai
    start_lesson_button = driver.find_element(AppiumBy.ID, "com.example.languageapp:id/start_lesson")
    start_lesson_button.click()
```


```
    time.sleep(2)
    answer_field = driver.find_element(AppiumBy.ID, "com.example.languageapp:id/answer_input")
    answer_field.send_keys("Wrong")
```


```
    submit_button = driver.find_element(AppiumBy.ID, "com.example.languageapp:id/submit_button")
    submit_button.click()
```


```
    time.sleep(2)
    error_message = driver.find_element(AppiumBy.ID, "com.example.languageapp:id/error_text")
    assert "Incorrect answer" in error_message.text
```


```
def test_navigation_to_profile(driver):
    # Test case: Kiểm tra chuyển đổi sang màn hình hồ sơ
    menu_button = driver.find_element(AppiumBy.ACCESSIBILITY_ID, "Menu")
    menu_button.click()
```


```
    time.sleep(1)
    profile_option = driver.find_element(AppiumBy.XPATH, "//android.widget.TextView[@text='Profile']")
    profile_option.click()
```


```
    time.sleep(1)
    profile_title = driver.find_element(AppiumBy.ID, "com.example.languageapp:id/profile_title")
    assert profile_title.is_displayed()
```

#### Gợi ý README.md

Dưới đây là một mẫu file README.md mà sinh viên có thể sử dụng:

# Appium Assignment (không bắt buộc)

## Ứng dụng được chọn

Tên ứng dụng: Duolingo

Danh mục con: Học ngoại ngữ

Lý do chọn: Dựa trên 2 chữ số cuối của MSSV (78 % 5 = 3, thuộc danh mục Học ngoại ngữ). Duolingo là ứng dụng phổ biến với các bài học ngôn ngữ tương tác, phù hợp để kiểm thử.

## Test Cases

Test Case 1: Hoàn thành bài học ngôn ngữ

Mô tả: Kiểm tra xem người dùng có thể hoàn thành một bài học và nhận kết quả đúng.

Kết quả mong đợi: Hiển thị thông báo "Correct!" sau khi trả lời đúng.

Test Case 2: Nhập câu trả lời sai

Mô tả: Kiểm tra xem ứng dụng có hiển thị thông báo lỗi khi nhập sai câu trả lời.

Kết quả mong đợi: Hiển thị thông báo "Incorrect answer".

Test Case 3: Chuyển đổi sang màn hình hồ sơ

Mô tả: Kiểm tra xem người dùng có thể chuyển từ menu chính sang màn hình hồ sơ.

Kết quả mong đợi: Màn hình hồ sơ hiển thị đúng.

## Hướng dẫn chạy kịch bản kiểm thử

Cài đặt môi trường:

Cài Appium Server: npm install -g appium

Cài Android Studio và thiết lập emulator (API 30).

Cài Python 3.8+ và các thư viện: pip install Appium-Python-Client pytest

Tải Duolingo APK từ [liên kết].

Chạy Appium Server: appium

Chạy kiểm thử: pytest test_language_app.py

## Kết quả kiểm thử

Test Case 1: Passed (xem ảnh chụp màn hình: screenshots/test1.png).

Test Case 2: Passed.

Test Case 3: Failed do lỗi hiển thị màn hình hồ sơ (xem video: videos/test3.mp4).

## Khó khăn và cách khắc phục

Khó khăn: Không tìm thấy phần tử bằng ID do ứng dụng thay đổi cấu trúc.

Cách khắc phục: Sử dụng Appium Inspector để tìm XPath thay thế.

## Link minh họa

Video demo chạy kiểm thử

Ảnh chụp màn hình

### Lưu ý

Sinh viên cần kiểm tra với bạn cùng lớp để đảm bảo không chọn trùng ứng dụng.

Nếu gặp khó khăn trong việc thiết lập môi trường, tham khảo tài liệu chính thức của Appium hoặc liên hệ giảng viên.

Đảm bảo repository GitHub có ít nhất 3 commit với thông điệp rõ ràng (ví dụ: "Khởi tạo dự án", "Thêm test case bài học", "Cập nhật README.md").


## V. Quản lý lỗi (Defect Management) với GitHub Issues và Jira (chuẩn doanh nghiệp)

### Mục tiêu học tập:

- Chuẩn hóa cách ghi nhận lỗi (bug/defect) theo mẫu doanh nghiệp: mô tả, bước tái hiện, bằng chứng, mức độ ảnh hưởng.

- Thực hành vòng đời lỗi (defect lifecycle): tạo - phân loại - ưu tiên - giao việc - sửa - kiểm tra lại - đóng.

- Sử dụng GitHub Issues để quản lý lỗi theo quy trình (label, assignee, milestone, project board, liên kết commit/PR).

- Làm quen Jira Software: tạo dự án, cấu hình issue type/workflow cơ bản, thực hiện triage và báo cáo số liệu.

### 1. Bối cảnh và phạm vi bài tập

Sinh viên chọn 1 trong 2 nguồn để tạo lỗi:

1. Dự án JUnit ở Bài I (StudentAnalyzer): cố tình tạo/ghi nhận lỗi logic, lỗi xử lý dữ liệu không hợp lệ, lỗi sai điều kiện biên.

2. Dự án Cypress ở Bài II (Saucedemo): ghi nhận lỗi theo kịch bản E2E (đăng nhập, giỏ hàng, thanh toán, sắp xếp).

Yêu cầu tối thiểu:

- Tạo ít nhất 8 defect (bug) có mô tả đầy đủ, trong đó tối thiểu 2 defect mức nghiêm trọng cao.

- Tạo ít nhất 4 work item không phải bug (task/improvement) liên quan đến chất lượng: bổ sung test, refactor, cập nhật tài liệu, cấu hình CI.

- Mỗi defect phải gắn bằng chứng: ảnh chụp màn hình, log, kết quả test (JUnit report/Cypress video), hoặc mô tả dữ liệu đầu vào gây lỗi.

- Mỗi defect khi được xử lý phải có liên kết đến commit hoặc pull request; có bước retest và trạng thái đóng rõ ràng.

### 2. Chuẩn hóa thuật ngữ, mức độ và quy ước

#### 2.1. Phân biệt Severity và Priority

Severity (mức nghiêm trọng) phản ánh mức độ ảnh hưởng kỹ thuật và tác động đến người dùng. Priority (mức ưu tiên) phản ánh thứ tự cần xử lý theo kế hoạch/kinh doanh.

Bảng Severity (tham khảo mẫu doanh nghiệp):

| Mức | Tên gọi | Mô tả/tiêu chí |
| --- | --- | --- |
| S1 | Critical | Ứng dụng không sử dụng được, crash/blocking luồng chính, mất dữ liệu hoặc lỗ hổng nghiêm trọng; không có workaround. |
| S2 | High | Chức năng chính sai nhưng còn workaround; ảnh hưởng nhiều người dùng; rủi ro cao. |
| S3 | Medium | Chức năng phụ sai; ảnh hưởng một phần; workaround dễ. |
| S4 | Low | Lỗi giao diện/hiển thị nhỏ, sai chính tả; ít ảnh hưởng. |

Bảng Priority (tham khảo mẫu doanh nghiệp):

| Mức | Tên gọi | Gợi ý thời điểm xử lý |
| --- | --- | --- |
| P0 | Immediate | Sửa ngay (hotfix) trước khi bàn giao/merge/release. |
| P1 | High | Sửa trong sprint/đợt gần nhất. |
| P2 | Normal | Sửa khi có thời gian; có thể gộp vào sprint sau. |
| P3 | Low | Có thể trì hoãn; cân nhắc WONTFIX nếu không đáng. |

#### 2.2. Quy ước đặt tiêu đề và phân loại lỗi

Tiêu đề issue theo mẫu:

- [BUG][Module] Mô tả ngắn gọn vấn đề (tối đa 12-15 từ)

- [TASK][Module] Mô tả công việc cải tiến/chất lượng

Module có thể là: StudentAnalyzer, JUnit, Cypress, Login, Cart, Checkout, CI, Docs.

Gợi ý label chuẩn:

- type: bug | task | improvement

- severity: S1 | S2 | S3 | S4

- priority: P0 | P1 | P2 | P3

- component: <module>

- status: triage | in-progress | ready-for-test | done

- env: local | staging | prod (nếu có)

#### 2.3. Vòng đời lỗi (Defect Lifecycle) khuyến nghị

1. New: ghi nhận lỗi, mô tả đầy đủ và đính kèm bằng chứng.

2. Triage: nhóm/giảng viên phân loại (severity/priority), xác nhận có phải lỗi thật, gán người xử lý.

3. In Progress: developer đang sửa, cập nhật nhánh/PR liên quan.

4. Ready for Test: đã có bản sửa (commit/PR merge hoặc build), chuyển QA/Reporter kiểm tra lại.

5. Re-test: chạy lại test case, xác minh đã hết lỗi; nếu chưa hết thì Reopen.

6. Done/Closed: lỗi đã được xác nhận khắc phục; cập nhật release note/known issue nếu cần.

7. Duplicate/Won't Fix/Cannot Reproduce: đóng theo lý do, vẫn lưu lịch sử và bằng chứng.

### 3. Thực hành quản lý lỗi với GitHub Issues

#### 3.1. Thiết lập repository

- Tạo repo theo định dạng: defect-mgmt-[HoTenKhongDau] hoặc dùng lại repo của Bài I/Bài II và tạo nhánh riêng.

- Tạo thư mục /docs để lưu tài liệu (mẫu báo cáo, ảnh bằng chứng, kết quả chạy test).

- Bật Issues và Projects (nếu dùng GitHub Projects).

#### 3.2. Tạo Issue Template theo mẫu doanh nghiệp

Tạo thư mục .github/ISSUE_TEMPLATE/ và thêm tối thiểu 2 template:

- Bug report (bắt buộc).

- Task/Improvement (bắt buộc).

Mẫu nội dung Bug report (Markdown):

File: .github/ISSUE_TEMPLATE/bug_report.md

```
---
name: Bug report
about: Báo lỗi theo mẫu doanh nghiệp
title: "[BUG][Module] ..."
labels: ["type: bug"]
assignees: []
---
```


```
## Mô tả
(Mô tả ngắn gọn vấn đề và tác động)
```


```
## Môi trường
- OS/Browser/Device:
- Version/Branch/Commit:
- Test data:
```


```
## Bước tái hiện (Steps to Reproduce)
1.
2.
3.
```


```
## Kết quả thực tế (Actual Result)
```


```
## Kết quả mong đợi (Expected Result)
```


```
## Bằng chứng (Evidence)
- Screenshot/Video:
- Log/Test report:
```


```
## Phân loại
- Severity: S?
- Priority: P?
- Component:
```


```
## Gợi ý nguyên nhân/đề xuất (nếu có)
```


#### 3.3. Thiết lập Project Board (Kanban)

Tạo board với các cột tối thiểu (mapping defect lifecycle):

- New

- Triage

- In Progress

- Ready for Test

- Done

Quy tắc vận hành:

- Issue mới phải có đầy đủ 4 phần: Steps, Actual, Expected, Evidence.

- Triage phải gán severity, priority, component, assignee và milestone/iteration (nếu có).

- Chỉ chuyển sang Ready for Test khi có link commit/PR và mô tả cách verify.

#### 3.4. Liên kết issue với commit/pull request

- Commit message/PR description dùng cú pháp: fixes #<id> hoặc closes #<id> để tự động đóng issue khi merge.

- Đặt tên nhánh gợi ý: bugfix/<id>-short-slug hoặc task/<id>-short-slug.

- Trong PR, mô tả: nguyên nhân, cách sửa, ảnh/chứng cứ test pass (JUnit/Cypress).

#### 3.5. Yêu cầu thực hiện

1. Tạo 8 issue loại Bug theo template và gán nhãn đầy đủ.

2. Tạo 4 issue loại Task/Improvement (bổ sung test case, CI, refactor, docs).

3. Chọn ít nhất 4 bug để thực hiện sửa: mỗi bug có 1 nhánh, 1 PR, 1 lần re-test, và đóng issue theo quy trình.

4. Xuất/ghi lại báo cáo số liệu: tổng bug theo severity, số bug đã đóng, lead time trung bình (tạo đến đóng).

### 4. Thực hành quản lý lỗi với Jira (mô phỏng quy trình doanh nghiệp)

#### 4.1. Thiết lập dự án Jira

- Tạo project dạng Kanban hoặc Scrum (tùy lựa chọn).

- Tạo issue types: Bug, Task, Story (tối thiểu Bug và Task).

- Thiết lập Components theo module (Login/Cart/Checkout/StudentAnalyzer...).

- Thiết lập Versions (ví dụ: v0.1, v0.2) để gán Fix Version.

#### 4.2. Trường thông tin khuyến nghị

| Trường | Bắt buộc? | Ghi chú |
| --- | --- | --- |
| Summary | Có | Tiêu đề ngắn gọn theo quy ước. |
| Description | Có | Bao gồm Steps/Actual/Expected/Evidence. |
| Environment | Có | OS/Browser/Device, build/branch/commit. |
| Severity | Có | S1-S4 (custom field hoặc label). |
| Priority | Có | P0-P3 (Priority mặc định của Jira hoặc custom). |
| Component/s | Có | Module bị ảnh hưởng. |
| Fix Version | Khuyến nghị | Phiên bản dự kiến sửa. |

#### 4.3. Workflow khuyến nghị

New → Triage → In Progress → Code Review → Ready for Test → Done (Reopen nếu fail retest).

#### 4.4. Yêu cầu thực hiện

1. Tạo tối thiểu 5 Bug và 2 Task trên Jira (có thể nhập lại từ GitHub).

2. Thực hiện triage cho toàn bộ Bug: gán severity, priority, component, assignee, fix version.

3. Tạo tối thiểu 2 filter JQL (ví dụ: Bug mức S1/S2 chưa Done; Bug theo component).

4. Tạo 1 dashboard đơn giản (nếu có quyền): biểu đồ bug theo severity và created vs resolved.

### 5. Tài liệu và biểu mẫu (mẫu doanh nghiệp)

Sinh viên nộp kèm các tài liệu dưới đây trong thư mục /docs của repository.

#### 5.1. Defect Management Plan (DMP) - đề cương tối thiểu

1. Mục tiêu và phạm vi

2. Công cụ sử dụng (GitHub/Jira) và cách đặt quyền truy cập

3. Vai trò và trách nhiệm (Reporter/QA/Dev/Lead)

4. Quy ước đặt tên, label, component, version

5. Định nghĩa Severity/Priority (bảng)

6. Workflow và tiêu chí chuyển trạng thái (Definition of Ready/Done cho bug)

7. Quy tắc triage (tần suất, ai tham gia, cách ra quyết định)

8. Tiêu chí đóng lỗi và quy tắc reopen

9. Số liệu theo dõi (KPIs) và nhịp báo cáo

#### 5.2. Mẫu báo lỗi (Bug/Defect Report)

| Defect ID | (Hệ thống tự sinh: #ID hoặc JIRA-123) |
| --- | --- |
| Title/Summary | [BUG][Module] ... |
| Reported by |  |
| Date/Time |  |
| Environment | OS/Browser/Device, build/branch/commit |
| Precondition | Tài khoản/ dữ liệu cần có trước khi chạy |
| Steps to Reproduce | 1...<br>2...<br>3... |
| Actual Result |  |
| Expected Result |  |
| Severity | S1/S2/S3/S4 |
| Priority | P0/P1/P2/P3 |
| Attachments/Evidence | Link ảnh/video/log/test report |
| Assignee/Owner |  |
| Status | New/Triage/In Progress/Ready for Test/Done/Reopen |

#### 5.3. Mẫu biên bản triage lỗi (Defect Triage Minutes)

| Thông tin cuộc họp | Ngày/giờ, thành phần, dự án/phiên bản |
| --- | --- |
| Mục tiêu | Xác nhận lỗi, phân loại severity/priority, quyết định xử lý |
| Danh sách lỗi xem xét | Link danh sách issue/JQL filter |
| Quyết định cho từng lỗi | Defect ID \| Quyết định (Fix/Duplicate/Won't Fix/Cannot Reproduce) \| Owner \| Due date |
| Rủi ro/ảnh hưởng | Lỗi blocking? ảnh hưởng release? |
| Hành động tiếp theo | Ai làm gì, deadline |
| Kết luận | Tổng số lỗi được duyệt/đóng/chuyển trạng thái |
| Người ghi biên bản |  |

#### 5.4. Mẫu báo cáo số liệu lỗi (Defect Metrics Report)

| Kỳ báo cáo | Tuần ... / Sprint ... (từ ... đến ...) |
| --- | --- |
| Tổng số defect tạo mới |  |
| Tổng số defect đã đóng |  |
| Defect tồn (open) theo severity | S1: ; S2: ; S3: ; S4: |
| Lead time trung bình | Trung bình (Created → Done) |
| Top 3 component nhiều lỗi |  |
| Tỷ lệ reopen |  |
| Nguyên nhân phổ biến | Ví dụ: thiếu validate, sai điều kiện biên, thiếu test |
| Rủi ro và đề xuất | Ví dụ: bổ sung regression test, tăng review |
| Người lập báo cáo |  |

#### 5.5. Mẫu phân tích nguyên nhân gốc (RCA - 5 Whys)

| Defect ID |  |
| --- | --- |
| Vấn đề |  |
| Tác động |  |
| Why #1 |  |
| Why #2 |  |
| Why #3 |  |
| Why #4 |  |
| Why #5 / Root Cause |  |

### 6. Quy trình nộp bài

- Repository GitHub: chứa Issues/Projects, mã nguồn (nếu có sửa), và thư mục /docs (DMP + các mẫu đã điền + bằng chứng).

- Ảnh chụp màn hình: board trạng thái, 1-2 issue bug hoàn chỉnh, PR có liên kết fixes #ID, kết quả test pass sau khi fix.

- Jira: nộp kèm file export (CSV/PDF) hoặc ảnh chụp màn hình board + 1 dashboard/filter.

- Nộp link repo (và link Jira nếu được chia sẻ) lên LMS theo đúng tên bài.

### 7. Tiêu chí đánh giá (tham khảo)

| Hạng mục | Mô tả | Tỷ trọng |
| --- | --- | --- |
| Chất lượng báo lỗi | Đủ Steps/Actual/Expected/Evidence; severity/priority hợp lý; tiêu đề/label chuẩn. | 40% |
| Quy trình xử lý | Có triage, assign, link PR/commit, retest, đóng issue đúng quy trình. | 25% |
| Tài liệu /docs | DMP + triage minutes + metrics report + RCA (đã điền) đầy đủ, trình bày rõ. | 20% |
| Jira | Tạo project/issue/workflow tối thiểu; có filter và minh chứng. | 15% |
