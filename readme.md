### So sánh các mô hình "RC Equivalent Circuit Models" cho "Lithium-Ion Batteries" cho xe điện "Electric Vehicles"


## Abstract
Equivalent circuit models là một chủ đề nghiên cứu nóng trong lĩnh vực pin lithium-ion cho xe điện, và các học giả đã đề xuất nhiều mô hình Equivalent circuit models từ đơn giản đến phức tạp. Một mặt, một mô hình đơn giản không thể simulation các đặc tính động của pin; Mặt khác, rất khó để áp dụng một mô hình phức tạps vào một hệ thống thời gian thực. Hiện tại, có rất ít nghiên cứu so sánh có hệ thống về các mô hình Equivalent circuit models của pin lithium-ion. Mô hình cụm 1RC thường được sử dụng trong tài liệu được nghiên cứu so sánh trong bài báo này. Thứ nhất, các thông số của hai mô hình được xác định bằng thực nghiệm; thứ hai, mô hình mô phỏng được xây dựng trong môi trường Matlab / Simulink, và cuối cùng độ chính xác đầu ra của hai mô hình này được xác minh bằng dữ liệu thực tế. Kết quả cho thấy trong điều kiện dòng điện không đổi, sai số lớn nhất của mô hình RC bậc một là 1,65% và sai số lớn nhất đối với mô hình RC bậc hai là 1,22%. Trong điều kiện lịch trình lái xe lực kế hoạch đô thị (UDDS), sai số tối đa của mô hình 1 RC là 1,88% và đối với mô hình RC bậc hai, sai số tối đa là 1,69%. Điều này có ý nghĩa hướng dẫn rất lớn đối với việc ứng dụng trong các hệ thống quản lý pin thực tế cho mô hình mạch tương đương của pin lithium-ion của xe điện.

## Giới thiệu

Pin Lithium-ion có nhiều ưu điểm, chẳng hạn như điện áp làm việc cao, khối lượng nhỏ, trọng lượng nhẹ, tuổi thọ dài, thân thiện với môi trường, hiệu ứng bộ nhớ yếu (weak memory effect), phạm vi nhiệt độ làm việc rộng, tốc độ tự xả thấp, v.v. [1,2,3,4]. Pin lithium-ion đã được sử dụng rộng rãi trong điện thoại di động, máy ảnh kỹ thuật số, máy tính xách tay, các thiết bị điện tử tiêu dùng di động khác và lưu trữ năng lượng tái tạo [5,6]. Với sự phát triển và cải tiến không ngừng của khoa học và công nghệ, phạm vi ứng dụng của pin lithium-ion đã mở rộng hơn nữa sang năng lượng điện, hàng không vũ trụ, quân sự và các lĩnh vực quan trọng khác [7,8]. Pin Lithium-ion đã trở thành thành phần cốt lõi của việc cung cấp năng lượng cho nhiều thiết bị hoặc hệ thống quan trọng và thường rất quan trọng đối với độ tin cậy và chức năng của hệ thống tổng thể [3,8]. Tuy nhiên, hậu quả khi pin có lỗi có thể từ sự bất tiện khi điện thoại hết pin đến những hậu quả nghiêm trọng hơn; ví dụ, Mars Global Surveyor của NASA ngừng chạy do hỏng pin vào tháng 11 năm 2006.

Độ tin cậy của hệ thống pin lithium-ion vẫn chưa được cải thiện. Gần đây, pin lithium-ion đã đạt đến mức độ triển khai cho phép sử dụng chúng trong các ứng dụng ô tô nghiêm ngặt; ví dụ, Nissan LEAF đã lăn bánh khỏi dây chuyền lắp ráp vào năm 2010 cũng như Tesla Roadster vào năm 2008 [9]. Pin lithium-ion ô tô thường bao gồm hàng trăm hoặc thậm chí hàng nghìn cells pin đơn được kết nối nối tiếp và song song nên chúng có công suất và mật độ năng lượng cao cùng với các vấn đề như an toàn, độ tin cậy và tính đồng nhất. Hiện tại, một hệ thống quản lý pin (BMS) hiệu quả và đáng tin cậy đã trở thành chìa khóa để đảm bảo hoạt động đáng tin cậy và an toàn của pin lithium-ion [10,11]; Có nhiều khía cạnh trong quá trình phát triển hệ thống quản lý pin, chẳng hạn như phân tích yêu cầu, mô hình hóa và mô phỏng, nghiên cứu chiến lược điều khiển và kiểm tra phần cứng trực tuyến, tất cả đều cần một mô hình có khả năng để xác định các đặc tính của pin lithium-ion.

Để dự đoán hành vi của pin, nhiều mô hình khác nhau đã được thiết lập, thường có thể được chia thành hai loại: electrochemical models và equivalent circuit models. Mặc dù electrochemical models giải thích rõ các yếu tố vật lý cơ bản trong bên trong của pin dựa trên các thông số và main electrochemical variables (các yếu tố quan trọng ảnh hưởng đến quá trình hoạt động của pin như: Voltage, Current, Ion Concentration, Temperature, Internal Resistance, State of Charge - SOC), nhưng độ chính xác của nó khi áp dụng vào hệ thống điều khiển xe còn hạn chế. Điều này do mô hình khá phức tạp và cần thu thập nhiều thông số động học thiết kế cũng như điện hóa trước đó.
Do đó, mô hình electrochemical model thường được sử dụng để hiểu quá trình phản ứng bên trong pin, đồng thời hướng dẫn thiết kế và sản xuất pin. Trong mô hình mạch tương đương (ECM), điện trở, điện dung và nguồn điện áp được sử dụng để mô tả quá trình sạc và xả, và mô hình được xây dựng trong miền tần số hoặc miền thời gian [14,15], trong đó mỗi thành phần có ý nghĩa vật lý rõ ràng, biểu thức toán học đơn giản, trực quan hơn và dễ xử lý. Nó đã được áp dụng rộng rãi trong việc ước tính trạng thái sạc (SOC), trạng thái sức khỏe (SOH) và trạng thái chức năng (SOF) cho pin lithium-ion. Các tài liệu [16] dựa trên mô hình RC (điện trở-tụ điện) bậc nhất về phát hiện ngắn mạch pin lithium-ion đã được khám phá. Tài liệu [17] đã sử dụng mô hình mạch tương đương 1 RC để ước tính điện trở của pin lithium-ion và điện áp hở mạch. Tài liệu tham khảo [18] đã sử dụng mô hình mạch tương đương 1 RC để mô hình hóa và mô phỏng bộ pin lithium-ion. Một mô hình mạch tương đương 1 RC đã được tạo và xác nhận cho một loại pin cụ thể bằng cách sử dụng Simulink MATLAB (MathWork, Inc., Natick, MA, USA) về phân bố nhiệt độ bên trong, điện áp hở mạch, sinh nhiệt và điện trở bên trong trong Tài liệu tham khảo [19,20]. Một phương pháp ước tính SOC dựa trên mô hình mạch tương đương 1 RC của pin lithium-ion đã được nghiên cứu trong [21,22,23].

Các nghiên cứu trong [24,25,26] đã khám phá phương pháp ước tính SOC dựa trên mô hình mạch tương đương RC bậc hai của pin lithium-ion. Tài liệu tham khảo [26,27,28] đã nghiên cứu ước tính SOH dựa trên các mô hình mạch tương đương RC bậc hai của pin lithium-ion. Ngoài ra, Tham khảo [29] đã sử dụng mô hình mạch tương đương của mô hình RC bậc hai để mô hình hóa pin lithium-ion. Có thể thấy rằng các thuật toán ước tính SOC và SOH dựa trên mô hình mạch tương đương là loại thuật toán ước tính quan trọng nhất trong hệ thống quản lý pin. Nhiều học giả đã đề xuất nhiều mô hình mạch tương đương, từ đơn giản đến phức tạp. Tuy nhiên, có rất ít nghiên cứu so sánh có hệ thống về các mô hình mạch tương đương của pin lithium-ion và các mô hình đơn giản không thể mô phỏng đầy đủ các đặc tính động của pin, trong khi rất khó áp dụng các mô hình phức tạp cho các hệ thống thời gian thực. Sự lựa chọn giữa các mô hình này là sự đánh đổi giữa độ phức tạp của mô hình hóa, độ chính xác và chi phí tính toán. Do đó, mô hình RC bậc một và mô hình RC bậc hai thường được sử dụng trong tài liệu được nghiên cứu so sánh trong bài báo này vì tính đơn giản và độ chính xác tương đối của chúng. Trong bài báo này, đầu tiên, các thông số của hai mô hình trên được xác định bằng các phương pháp thí nghiệm riêng lẻ, sau đó các mô hình mô phỏng được xây dựng trong môi trường Matlab / Simulink, và cuối cùng độ chính xác của kết quả cho hai mô hình được xác minh và thảo luận so sánh với dữ liệu thực tế.

## 2 Experiments and Methods
### 2.1. ECM for Lithium-Ion Batteries

Các mô hình mạch tương đương sử dụng mạch bao gồm voltage sources, resistors, và capacitors để mô phỏng các đặc tính động của pin [14,15], do đó mô tả mối quan hệ giữa điện áp và dòng điện được thể hiện trong hoạt động của pin. Trong bài báo này, mô hình RC bậc một và mô hình RC bậc hai được nghiên cứu tương đối, vì chúng chủ yếu đề cập đến các mô hình mạch tương đương được sử dụng trong tài liệu. Một mặt, hai loại mô hình này thực hiện tốt công việc phản ánh các đặc tính động và tĩnh của pin lithium-ion, mặt khác độ phức tạp của các mô hình cũng phù hợp, dễ thực hiện trong kỹ thuật và dễ dàng thực hiện nhận dạng thông số với độ chính xác cao.

Sơ đồ của mô hình 1 RC được thể hiện trong Hình 1a, trong đó điện áp có thể điều khiển VOC biểu thị điện áp hở mạch của pin lithium-ion thường thay đổi phi tuyến tính với SOC, R0 biểu thị điện trở ohmic của pin lithium-ion mô tả điện trở điện phân và điện trở kết nối của pin, R1 biểu thị điện trở phân cực, C1 biểu thị điện dung phân cực, I biểu thị dòng điện chạy qua tải có thể được đo trực tiếp từ cảm biến dòng điện và U biểu thị điện áp đầu cuối của pin có thể được đo trực tiếp từ cảm biến điện áp. Mạng RC song song mô tả phản ứng phân cực phi tuyến của pin lithium-ion và I dương khi xả và âm cho sạc.

-------- Hình 1 --------

Sơ đồ của mô hình RC bậc hai được thể hiện trong Hình 1b, trong đó VOC R0, I và bạn có ý nghĩa giống như trong mô hình RC bậc một, ngoại trừ việc có hai mạng RC song song để mô tả phản ứng phân cực phi tuyến của pin lithium-ion.

### 2.2. Battery Testing Bench

Để hoàn thành việc xác định thông số mô hình, băng thử nghiệm được hiển thị trong Hình 2 đã được thiết lập. Nó bao gồm một hệ thống kiểm tra pin NEWARE (NEWARE Co., Limited, Thâm Quyến, Trung Quốc) 4000 (BTS4000) với tám kênh độc lập, một máy trung gian và một máy tính chủ có cài đặt Phần mềm NEWARE BTS v7.5.6 và MATLAB R2010a.

Máy kiểm tra pin được sử dụng để tải các cấu hình dòng điện được lập trình trên pin trong phạm vi điện áp 0–10 V và dòng điện −6 đến 6 A, đồng thời sai số đo của cảm biến điện áp và dòng điện của nó đều nhỏ hơn 0,5%. Máy trung gian chịu trách nhiệm chính về kết nối mạng, nhận lệnh điều khiển từ máy tính chủ, điều khiển bộ luân chuyển pin thấp hơn và tải lên dữ liệu kiểm tra thời gian thực. Máy tính chủ được sử dụng để điều khiển và giám sát máy quay vòng thông qua cáp Ethernet, cũng như để lưu trữ điện áp và dòng điện mà các cảm biến thu được. Các tế bào pin được thử nghiệm là các tế bào hình trụ 18650 đại diện có thông số kỹ thuật chủ yếu bao gồm dung lượng danh nghĩa 2350 mAh, điện áp hoạt động 3,7 V, điện áp giới hạn sạc 4,2 V, điện áp giới hạn phóng điện 2,7 V và dòng xả liên tục tối đa 10 A. Trong quá trình thử nghiệm, dòng điện và điện áp của pin được ghi lại mỗi giây, trong khi chúng được ghi lại cứ sau 100 mili giây trong quá trình kiểm tra đặc tính công suất xung lai (HPPC). Các thông số quan trọng của thí nghiệm được tóm tắt trong Bảng 1.

---- Table 1 ----

### 2.3. Model Parameter Identification
open circuit voltage (OCV) của pin là giá trị điện áp ổn định của pin khi để pin ở trạng thái hở mạch [11]. Đối với ắc quy sau khi được sạc, điện áp cực ắc quy sẽ giảm dần về giá trị ổn định khi để ở trạng thái hở mạch; Đối với ắc quy sau khi phóng điện, điện áp cực ắc quy sẽ tăng dần đến giá trị ổn định sau khi dỡ tải. Sức điện động của pin về cơ bản bằng điện áp hở mạch của pin, trong khi suất điện động của pin là một trong những thước đo dùng để đo lượng năng lượng dự trữ trong pin. Như vậy, có một mối quan hệ nhất định giữa OCV của pin và SOC của pin [22]. Có một số cách để thu được OCV, trong đó phương pháp tĩnh là phương pháp trực tiếp và tương đối chính xác hơn. Để có được mối quan hệ giữa OCV của pin và SOC trong phương pháp đứng yên, quy trình kiểm tra được thực hiện như sau [30]:

(1) Hiệu chỉnh dung lượng pin. Pin được sạc đầy bằng phương pháp sạc tiêu chuẩn, trong đó pin được sạc bằng pha dòng điện không đổi từ 2,35 A (1C) đến 4,2 V, sau đó là pha điện áp không đổi 4,2 V cho đến khi dòng điện giảm xuống 0,02 A. Sau đó , pin được phóng điện với pha dòng điện không đổi 2,35 A đến điện áp cắt phóng điện 2,7 V. Thí nghiệm được lặp lại cho đến khi chênh lệch giữa công suất phóng điện của mỗi phép đo không vượt quá 2% và thì dung lượng đo được coi là dung lượng thực tế của pin.

(2) Pin được sạc đầy bằng phương pháp sạc tiêu chuẩn được mô tả ở Bước (1) và sau đó pin được để ở trạng thái mạch hở để nghỉ trong 4 giờ để đạt được trạng thái cân bằng điện hóa và nhiệt [9].

(3) Pin được xả với dòng điện không đổi 2,35 A trong 6 phút (tức là xả 10% dung lượng) và sau đó pin được để ở điều kiện mạch hở để nghỉ trong 4 giờ để đạt được trạng thái cân bằng điện hóa và nhiệt.

(4) Bước (3) được lặp lại 8 lần.

(5) Pin được xả với dòng điện không đổi 2,35 A trong 3 phút (tức là xả 10% dung lượng) và sau đó pin được để ở điều kiện mạch hở trong 4 giờ để đạt được trạng thái cân bằng điện hóa và nhiệt.

(6) Bước (5) được lặp lại bốn lần.

Trong các thử nghiệm, điện áp đo được ở cuối mỗi giai đoạn chờ được coi là điện áp mạch hở cuối cùng. Sự biến đổi của OCV với SOC thu được bằng phương pháp thử nghiệm ở trên được thể hiện trong Hình 3.

### 2.3.2. Ohmic Resistance
Nói chung, các phương pháp được sử dụng để đo điện trở của pin là phương pháp tắt nguồn, phương pháp từng bước và phương pháp quang phổ trở kháng điện hóa (EIS). Với phương pháp EIS, pin được kích thích bởi một loạt tín hiệu dòng điện xoay chiều (AC) có tần số khác nhau, sau đó thông qua phân tích mối quan hệ giữa tín hiệu kích thích đầu vào và đáp ứng điện áp đầu ra của pin, từ đó có thể thu được đặc tính trở kháng của pin. Nguyên lý của phương pháp tắt nguồn và phương pháp từng bước là tương tự nhau, trong đó sự khác biệt giữa thời gian đáp ứng phân cực ohm và thời gian đáp ứng phân cực khác được sử dụng để xác định trở kháng khác nhau. Khi dòng điện thay đổi đột ngột, phần sụt áp do phân cực ohm gây ra sẽ thay đổi tức thời và sau đó phần sụt áp do phân cực khác hoàn thành quá trình nhất thời với hàm mũ gần đúng cho đến khi điện áp trở về giá trị điện áp ở trạng thái ổn định. Giả sử điện áp trước khi dòng điện thay đổi là U0 và điện áp sau thời điểm dòng điện thay đổi là U1 thì công thức tính điện trở Ohm như sau:

                R0(SOC)=U1−U0/ΔI

Đề cập đến bài kiểm tra đặc tính công suất xung lai “Sổ tay kiểm tra pin CAR Freedom” (thử nghiệm HPPC) [31], bài viết này áp dụng phương pháp từng bước để thu được điện trở ohmic, điện trở phân cực và điện dung phân cực từ các SOC khác nhau. Cấu hình kiểm tra đặc tính công suất xung lai được hiển thị trong Hình 4.

-------Figure 4. Hybrid pulse power characterization (HPPC) test current profile------

Để thu được ohmic resistance, polarization resistance, và polarization capacitance tại các SOC khác nhau, các thử nghiệm được thực hiện như sau:

(1) Hiệu chỉnh dung lượng pin như mô tả trong Mục 2.3.1.

(2) Sạc đầy pin bằng phương pháp sạc tiêu chuẩn giống như được mô tả trong Phần 2.2.

(3) Thử nghiệm HPPC được thực hiện và sau đó pin được để ở trạng thái mạch hở để nghỉ trong 4 giờ để đạt được trạng thái cân bằng điện hóa và nhiệt [9].

(4) Pin được xả với dòng điện không đổi 2,35 A trong 6 phút và sau đó pin được để ở trạng thái mạch hở để nghỉ trong 4 giờ để đạt được trạng thái cân bằng điện hóa và nhiệt.

(5) Bước (3) và (4) lần lượt được lặp lại tám lần.

(6) Pin được phóng điện với dòng điện không đổi 2,35 A trong 3 phút và sau đó pin được để ở trạng thái mạch hở để nghỉ trong 4 giờ để đạt được trạng thái cân bằng điện hóa và nhiệt.

(7) Thử nghiệm HPPC được thực hiện và sau đó pin được để ở trạng thái mạch hở để nghỉ trong 4 giờ để đạt được trạng thái cân bằng điện hóa và nhiệt.

(8) Bước (6) và (7) lần lượt được lặp lại bốn lần.

Từ các bước thử nghiệm trên, có thể thấy rằng thử nghiệm HPPC có thể được thực hiện cùng với thử nghiệm điện áp mạch hở được mô tả ở Mục 2.3.1. Theo các quy trình thử nghiệm ở trên, có thể thu được đường cong đáp ứng điện áp của pin lithium-ion được kích thích bằng thử nghiệm HPPC ở các SOC khác nhau. Kết quả được thể hiện trong Hình 5. Sau đó, điện trở ohmic ở các SOC khác nhau có thể tính được bằng cách tính Công thức (1). Kết quả được thể hiện ở Hình 6.
