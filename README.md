----------------Laravel 8----------------
Windows:
    <br>
  - install Git Bash: https://git-scm.com/downloads
    <br>
  -  install Xampp: https://www.apachefriends.org/download.html
    <br>
  -  install composer: https://getcomposer.org/download/


===  Một thuật toán gợi ý sản phẩm được tìm kiếm nhiều trong Laravel ===
- Bước 1: Lấy danh sách các sản phẩm được tìm kiếm nhiều
Để làm được điều này, bạn có thể sử dụng một truy vấn SQL để lấy các sản phẩm được tìm kiếm nhiều nhất từ cơ sở dữ liệu. Đối với ví dụ này, chúng ta sẽ giả định rằng mỗi lần tìm kiếm sản phẩm được lưu vào cơ sở dữ liệu như một bản ghi trong bảng 'search_logs'. Các bản ghi trong bảng này chứa thông tin về sản phẩm đã được tìm kiếm và số lần tìm kiếm.
Bước 2: Hiển thị danh sách các sản phẩm gợi ý
Sau khi đã có danh sách các sản phẩm được tìm kiếm nhiều nhất, bạn có thể hiển thị chúng trên trang web của mình.

====   Thuật toán gợi ý sản phẩm liên quan theo tỉ lệ gần đúng (%) ===
- Các thuật toán sử dụng là Khoảng cách Hamming cho các tính năng của sản phẩm, Khoảng cách Euclidean cho giá sản phẩm và hệ số tương tự Jaccard cho các danh mục sản phẩm.

+ hàm hamming(string $string1, string $string2, bool $returnDistance = false):  Tính toán độ đo tương đồng Hamming giữa hai chuỗi ký tự. Phương thức này nhận ba tham số: $string1 và $string2 là chuỗi cần tính toán, và $returnDistance là một biến boolean để quyết định phương thức sẽ trả về độ đo tương đồng hay khoảng cách giữa hai chuỗi. Độ đo Hamming là số lượng ký tự khác nhau giữa hai chuỗi.

+ hàm euclidean(array $array1, array $array2, bool $returnDistance = false): Tính toán khoảng cách Euclidean giữa hai mảng. Phương thức này nhận ba tham số: $array1 và $array2 là hai mảng cần tính toán, và $returnDistance là một biến boolean để quyết định phương thức sẽ trả về khoảng cách hay độ đo tương đồng giữa hai mảng. Khoảng cách Euclidean là căn bậc hai của tổng bình phương của hiệu giữa các phần tử tương ứng của hai mảng

+ hàm  jaccard(string $string1, string $string2, string $separator = ','): Tính toán độ đo tương đồng Jaccard giữa hai chuỗi được phân tách bằng một ký tự phân tách (mặc định là dấu phẩy). Phương thức này nhận ba tham số: $string1 và $string2 là hai chuỗi cần tính toán, và $separator là một ký tự phân tách. Độ đo Jaccard được tính bằng số phần tử chung giữa hai tập hợp chia cho số phần tử của tập hợp hợp của hai tập.

+ hàm minMaxNorm(array $values, $min = null, $max = null):Chuẩn hóa một mảng giá trị bằng cách chuyển đổi giá trị của mỗi phần tử trong mảng vào khoảng giá trị từ 0 đến 1. Phương thức này nhận ba tham số: $values là mảng giá trị cần chuẩn hóa, $min và $max là giá trị tối thiểu và tối đa của mảng. Nếu không có $min hoặc $max được cung cấp, chúng sẽ được tính toán dựa trên giá trị của mảng đầu vào. Chuẩn hóa được tính bằng cách trừ giá trị tối thiểu và chia cho khoảng giá trị của mảng.

+ Hàm getProductsSortedBySimularity(int $productId, array $matrix) dùng để sắp xếp các sản phẩm theo độ tương đồng với sản phẩm có ID là $productId.

- Bước đầu tiên, nó lấy ra các độ tương đồng của sản phẩm có ID là $productId từ ma trận $matrix, nếu không tìm thấy sản phẩm thì nó sẽ throw một exception.
Sau đó, nó sẽ sắp xếp các sản phẩm theo độ tương đồng giảm dần.
Với mỗi sản phẩm trong danh sách đã sắp xếp, nó lấy ra thông tin của sản phẩm đó và tính toán độ tương đồng với sản phẩm có ID là $productId, sau đó đưa sản phẩm đó vào một mảng $sortedProducts và trả về mảng này khi đã duyệt qua toàn bộ danh sách.
+ Hàm calculateSimilarityScore($productA, $productB) dùng để tính toán độ tương đồng giữa hai sản phẩm $productA và $productB dựa trên các tính năng khác nhau của sản phẩm.

- Đầu tiên, nó tạo ra hai object $featuresA và $featuresB chứa các thông tin về trọng lượng, tác giả, nhà xuất bản và số trang của hai sản phẩm.
Sau đó, nó chuyển đổi các object này thành một chuỗi string bằng cách lấy tất cả các thuộc tính của object và ghép lại với nhau.
Tiếp theo, nó sử dụng các hàm Similarity để tính toán độ tương đồng của các tính năng khác nhau của hai sản phẩm, sau đó cộng tổng các giá trị này lại để ra được độ tương đồng tổng thể của hai sản phẩm.
Cuối cùng, nó trả về giá trị độ tương đồng được tính toán này.


===  In PDF đơn hàng ===
- Hàm generatePDF($id) sử dụng thư viện PDF để tạo ra một file PDF từ dữ liệu đơn hàng và chi tiết đơn hàng.

===  Giảm giá ===
- Hàm addCouponCart() dùng để thêm mã giảm giá cho giỏ hàng của người dùng khi người dùng add mã giảm giá.
- Hàm getTotal() dùng để tính tổng giá trị của các sản phẩm trong giỏ hàng.
