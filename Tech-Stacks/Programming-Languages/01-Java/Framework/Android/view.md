- [View (class cơ bản đại diện cho một thành phần giao diện)](#view-class-cơ-bản-đại-diện-cho-một-thành-phần-giao-diện)
    - [View.OnClickListener](#viewonclicklistener)
- [AdapterView (là một loại View dùng để hiển thị một danh sách dữ liệu. Nó không tự tạo ra dữ liệu mà nhận dữ liệu thông qua một Adapter)](#adapterview-là-một-loại-view-dùng-để-hiển-thị-một-danh-sách-dữ-liệu-nó-không-tự-tạo-ra-dữ-liệu-mà-nhận-dữ-liệu-thông-qua-một-adapter)
---
# View (class cơ bản đại diện cho một thành phần giao diện)
### View.OnClickListener
MenuInflater
MenuItem
Menu
getItemId
# AdapterView (là một loại View dùng để hiển thị một danh sách dữ liệu. Nó không tự tạo ra dữ liệu mà nhận dữ liệu thông qua một Adapter)

Ví dụ bạn có danh sách 3 phòng ban:
ArrayList<PhongBan> dsPhongBan = new ArrayList<>();

dsPhongBan.add(new PhongBan("PB01", "Kế toán"));
dsPhongBan.add(new PhongBan("PB02", "Nhân sự"));
dsPhongBan.add(new PhongBan("PB03", "Kỹ thuật"));


Bạn muốn hiển thị danh sách này lên màn hình Android. Khi đó:
- ArrayList: chứa dữ liệu phòng ban.
- Adapter: lấy dữ liệu và chuyển thành giao diện từng dòng.
- AdapterView: nơi hiển thị các dòng dữ liệu đó.
ArrayList – Dữ liệu

PB01 – Kế toán · PB02 – Nhân sự · PB03 – Kỹ thuật

Adapter – Cầu nối

Lấy dữ liệu, tạo giao diện cho từng dòng

AdapterView – Nơi hiển thị
PB01

 Kế toán


PB02

Nhân sự


PB03

Kỹ thuật




Ví dụ những thành phần thuộc nhóm AdapterView thường gặp:
- ListView: hiển thị danh sách theo chiều dọc.
- GridView: hiển thị dữ liệu dạng lưới.
- Spinner: hiển thị danh sách lựa chọn dạng xổ xuống.
Trong bài của bạn, chúng ta chủ yếu dùng ListView.
2. AdapterView có những lệnh nào hay dùng?
Bạn không cần học thuộc toàn bộ. Với bài thi quản lý phòng ban, hãy tập trung vào các lệnh sau.
2.1. setAdapter() – Gắn Adapter vào ListView
Cú pháp:
listView.setAdapter(adapter);


Ý nghĩa: Gắn Adapter vào ListView để nó biết lấy dữ liệu nào và hiển thị như thế nào.

Ví dụ:
ArrayAdapter<String> adapter = new ArrayAdapter<>(
    this,
    android.R.layout.simple_list_item_1,
    dsTenPhongBan
);

listView.setAdapter(adapter);


Hiểu đơn giản:
- dsTenPhongBan: danh sách dữ liệu.
- adapter: cầu nối dữ liệu với giao diện.
- listView: nơi hiển thị danh sách.
2.2. setOnItemClickListener() – Bắt sự kiện nhấn vào một dòng
Khi người dùng nhấn vào một dòng trong ListView, hàm này sẽ được gọi.

Cú pháp:
listView.setOnItemClickListener(
    new AdapterView.OnItemClickListener() {
        @Override
        public void onItemClick(
            AdapterView<?> parent,
            View view,
            int position,
            long id
        ) {
            // Xử lý khi nhấn vào dòng
        }
    }
);


Có 4 tham số quan trọng:
Tham số	Ý nghĩa
parent	AdapterView chứa dòng vừa nhấn (ví dụ ListView)
view	Giao diện của dòng vừa nhấn
position	Vị trí dòng được nhấn
id	ID của dòng dữ liệu, thường do Adapter cung cấp

Ví dụ dễ hiểu nhất:
listView.setOnItemClickListener(
    new AdapterView.OnItemClickListener() {
        @Override
        public void onItemClick(
            AdapterView<?> parent,
            View view,
            int position,
            long id
        ) {
            String ten = dsTenPhongBan.get(position);

            Toast.makeText(
                MainActivity.this,
                "Bạn chọn: " + ten,
                Toast.LENGTH_SHORT
            ).show();
        }
    }
);


Nếu nhấn vào dòng thứ hai, position = 1 và chương trình lấy được phòng ban thứ hai.
Cần nhớ khi đi thi
position bắt đầu từ 0, không phải 1.
2.3. setOnItemLongClickListener() – Bắt sự kiện nhấn giữ một dòng
Lệnh này dùng khi người dùng nhấn giữ một dòng trong ListView.

Ví dụ: Nhấn giữ phòng ban để hiện menu Xóa, Sửa.

Cú pháp:
listView.setOnItemLongClickListener(
    new AdapterView.OnItemLongClickListener() {
        @Override
        public boolean onItemLongClick(
            AdapterView<?> parent,
            View view,
            int position,
            long id
        ) {
            // Xử lý khi nhấn giữ

            return true;
        }
    }
);


Ví dụ:
listView.setOnItemLongClickListener(
    new AdapterView.OnItemLongClickListener() {
        @Override
        public boolean onItemLongClick(
            AdapterView<?> parent,
            View view,
            int position,
            long id
        ) {
            String ten = dsTenPhongBan.get(position);

            Toast.makeText(
                MainActivity.this,
                "Bạn đang giữ: " + ten,
                Toast.LENGTH_SHORT
            ).show();

            return true;
        }
    }
);


Tại sao phải return true?
- true: Đã xử lý sự kiện nhấn giữ, Android không cần xử lý tiếp sự kiện này.
- false: Chưa xử lý xong, cho phép sự kiện tiếp tục được truyền đi.
Phân biệt hai lệnh:
Lệnh	Khi nào chạy?
setOnItemClickListener()	Nhấn một lần
setOnItemLongClickListener()	Nhấn giữ

2.4. getItemAtPosition() – Lấy dữ liệu tại một vị trí
Lệnh này lấy dữ liệu tương ứng với vị trí được chọn từ AdapterView.

Cú pháp:
Object data = parent.getItemAtPosition(position);


Ví dụ:
listView.setOnItemClickListener(
    new AdapterView.OnItemClickListener() {
        @Override
        public void onItemClick(
            AdapterView<?> parent,
            View view,
            int position,
            long id
        ) {
            String ten = (String) parent.getItemAtPosition(position);

            Toast.makeText(
                MainActivity.this,
                ten,
                Toast.LENGTH_SHORT
            ).show();
        }
    }
);


Nếu Adapter chứa String, ta ép kiểu sang String.

Nếu Adapter chứa PhongBan, ta ép kiểu sang PhongBan:
PhongBan pb = (PhongBan) parent.getItemAtPosition(position);


2.5. getSelectedItemPosition() – Lấy vị trí đang được chọn
Lệnh này thường dùng với các thành phần có lựa chọn như Spinner.

Cú pháp:
int position = spinner.getSelectedItemPosition();


Ví dụ:
int viTri = spinner.getSelectedItemPosition();

String ten = dsTenPhongBan.get(viTri);


Nếu Spinner đang chọn phòng ban thứ hai thì viTri = 1.

Lưu ý: ListView không hoạt động giống Spinner về trạng thái lựa chọn; khi nhấn một dòng, thường dùng trực tiếp position trong onItemClick().
2.6. getCount() – Lấy số lượng dòng
Lệnh này lấy số lượng phần tử mà AdapterView đang hiển thị.

Cú pháp:
int soLuong = adapterView.getCount();


Ví dụ:
int soLuong = listView.getCount();

Toast.makeText(
    this,
    "Số dòng: " + soLuong,
    Toast.LENGTH_SHORT
).show();


Nếu ListView có Header thì số dòng này có thể bao gồm cả Header.
3. Riêng ListView có một số lệnh rất hay dùng
Trong bài quản lý phòng ban của bạn, ngoài các lệnh trên, cần biết thêm:
Lệnh	Công dụng
addHeaderView(view)	Thêm dòng tiêu đề lên đầu danh sách
getHeaderViewsCount()	Lấy số lượng Header
setAdapter(adapter)	Gắn Adapter
setOnItemClickListener()	Bắt sự kiện nhấn dòng
setOnItemLongClickListener()	Bắt sự kiện nhấn giữ
getAdapter()	Lấy Adapter hiện tại

Ví dụ quan trọng khi ListView có Header:
int index = position - listView.getHeaderViewsCount();


Tại sao phải trừ?

Giả sử danh sách có một Header:
position của ListView	Nội dung	index trong ArrayList
0	Tiêu đề bảng	Không có
1	Phòng ban PB01	0
2	Phòng ban PB02	1
3	Phòng ban PB03	2

Vì vậy, khi nhấn phòng ban PB01, position = 1 nhưng vị trí trong ArrayList là 0.

Ta phải trừ số lượng Header để lấy đúng dữ liệu.
4. Ví dụ tổng hợp dễ hiểu nhất
Giả sử bạn có danh sách tên phòng ban và muốn hiển thị, nhấn vào để xem tên, nhấn giữ để xóa.
public class MainActivity extends AppCompatActivity {

    ListView lvPhongBan;

    ArrayList<String> dsPhongBan = new ArrayList<>();

    ArrayAdapter<String> adapter;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        // Bước 1: Ánh xạ ListView
        lvPhongBan = findViewById(R.id.lvPhongBan);

        // Bước 2: Thêm dữ liệu
        dsPhongBan.add("Kế toán");
        dsPhongBan.add("Nhân sự");
        dsPhongBan.add("Kỹ thuật");

        // Bước 3: Tạo Adapter
        adapter = new ArrayAdapter<>(
            this,
            android.R.layout.simple_list_item_1,
            dsPhongBan
        );

        // Bước 4: Gắn Adapter vào ListView
        lvPhongBan.setAdapter(adapter);

        // Bước 5: Sự kiện nhấn một lần
        lvPhongBan.setOnItemClickListener(
            new AdapterView.OnItemClickListener() {
                @Override
                public void onItemClick(
                    AdapterView<?> parent,
                    View view,
                    int position,
                    long id
                ) {
                    String ten = dsPhongBan.get(position);

                    Toast.makeText(
                        MainActivity.this,
                        "Bạn chọn: " + ten,
                        Toast.LENGTH_SHORT
                    ).show();
                }
            }
        );

        // Bước 6: Sự kiện nhấn giữ
        lvPhongBan.setOnItemLongClickListener(
            new AdapterView.OnItemLongClickListener() {
                @Override
                public boolean onItemLongClick(
                    AdapterView<?> parent,
                    View view,
                    int position,
                    long id
                ) {
                    // Xóa phần tử được nhấn giữ
                    dsPhongBan.remove(position);

                    // Cập nhật lại giao diện
                    adapter.notifyDataSetChanged();

                    return true;
                }
            }
        );
    }
}


5. Tổng kết: Đi thi cần nhớ gì?
Bạn chỉ cần nhớ 3 thành phần:
1. AdapterView

Nơi hiển thị danh sách, ví dụ ListView.

2. Adapter

Cầu nối giữa dữ liệu và giao diện.

3. Data

Dữ liệu cần hiển thị, ví dụ ArrayList<PhongBan>.

Và học thuộc 4 lệnh quan trọng nhất:
listView.setAdapter(adapter);             // Hiển thị dữ liệu

listView.setOnItemClickListener(...);      // Nhấn một lần

listView.setOnItemLongClickListener(...);  // Nhấn giữ

parent.getItemAtPosition(position);        // Lấy dữ liệu tại vị trí


Một mẹo học: Trong bài quản lý Phòng ban – Nhân viên, bạn hãy tập trung vào ListView, ArrayAdapter, setOnItemClickListener() và setOnItemLongClickListener() trước. Đây là nhóm kiến thức bạn sẽ sử dụng nhiều nhất.
Đúng rồi! AdapterView nằm trong package:
import android.widget.AdapterView;


Còn ArrayAdapter nằm trong package:
import android.widget.ArrayAdapter;


Hai cái này có quan hệ với nhau, nhưng không phải hai thứ thay thế cho nhau.
1. Tại sao không dùng ArrayAdapter mà phải dùng AdapterView?
Bạn hãy tưởng tượng việc hiển thị danh sách phòng ban giống như một cửa hàng:
- ArrayList<PhongBan>: Kho chứa dữ liệu phòng ban.
- ArrayAdapter: Người lấy dữ liệu từ kho, sắp xếp thành từng dòng giao diện.
- AdapterView: Cái kệ để trưng bày các dòng dữ liệu.
**ArrayList

**ArrayAdapter

ListView (AdapterView)

Hiển thị danh sách lên màn hình


Vậy nên:
- ArrayAdapter chịu trách nhiệm cung cấp dữ liệu và tạo giao diện.
- AdapterView chịu trách nhiệm hiển thị dữ liệu và nhận các sự kiện tương tác với các dòng.
2. Tại sao setOnItemClickListener lại thuộc AdapterView?
Bởi vì việc nhấn vào một dòng là hành động tương tác với danh sách đang hiển thị.

Ví dụ:
lvpb.setOnItemClickListener(
    new AdapterView.OnItemClickListener() {
        @Override
        public void onItemClick(
            AdapterView<?> parent,
            View view,
            int position,
            long id
        ) {
            // Xử lý khi nhấn vào một phòng ban
        }
    }
);


Ở đây:
- lvpb: Là ListView, nơi người dùng nhấn.
- AdapterView.OnItemClickListener: Là giao diện quy định cách xử lý sự kiện nhấn dòng.
- onItemClick(): Hàm được gọi khi người dùng nhấn một dòng.
Vậy tại sao không viết ArrayAdapter.OnItemClickListener?

Vì ArrayAdapter không phải nơi trực tiếp nhận thao tác nhấn trên danh sách. Nó chỉ cung cấp dữ liệu cho ListView.
3. Một điểm rất dễ nhầm: ListView cũng là AdapterView
Quan hệ kế thừa của chúng như sau:
AdapterView

Lớp cha

ListView

Lớp con

Các dòng dữ liệu


Vì ListView kế thừa AdapterView, nên ListView sử dụng được các phương thức và kiểu Listener được định nghĩa trong AdapterView.
4. Vậy khi nào dùng cái nào?
Thành phần	Dùng để làm gì?
ArrayList	Lưu danh sách dữ liệu
ArrayAdapter	Đưa dữ liệu vào giao diện
AdapterView	Quản lý kiểu danh sách và sự kiện tương tác
ListView	Hiển thị danh sách cụ thể

Mẹo nhớ khi đi thi:
- Muốn hiển thị dữ liệu → dùng ArrayAdapter.
- Muốn bắt sự kiện nhấn dòng → dùng AdapterView.OnItemClickListener.
- Muốn bắt sự kiện nhấn giữ dòng → dùng AdapterView.OnItemLongClickListener.
Bạn không phải chọn một trong hai. Trong một bài ListView thông thường, bạn sẽ sử dụng cả ArrayAdapter và AdapterView cùng lúc.