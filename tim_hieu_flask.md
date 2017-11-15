
## 1. Phân biệt Web và web service

- Khi ta gõ một URL vào trình duyệt và sẽ nhận được một trang web
- Như vậy, Web là giao diện tương tác với người dùng, cung cấp thông tin cho người dùng đầu cuối, thông tin ở dạng dễ đọc đối với con người
- Webservice là một dịch vụ của web, cung cấp thông tin cho người dùng ở dạng thô, khó hiểu, thông qua các ứng dụng sẽ xử lý dữ liệu thô trước khi trả kết quả cho người dùng.

## 2. Restful service

REST(REpresentation State Transfer) là một mô hình kiến trúc để thiết kế web service,được sử dụng trong việc giao tiếp giữa các máy tính(client-server) trong việc quản lý tài nguyên. nó định nghĩa các quy tắc để thiết kết các web service chú trọng vào tài nguyên hệ thống.

Rest hoạt động theo mô hình client-server, trong đó server bao gồm các service nhỏ nhận các request từ client.

Trong REST mọi thứ đều có thể coi là tài nguyên: tệp văn bản, ảnh, trang html, video, dữ liệu động,...

REST tuân thủ theo 4 nguyền tắc cơ bản để cài đặt 1 RESTful service:
+ Sử dụng các phương thức của HTTP
+ Phi trạng thái
+ Hiển thị các cấu trúc thư mục - URIs
+ Truyền tải XML, JSON hoặc cả hai

### a. Sử dụng các phương thức của HTTP

REST xác định rõ các chức năng của từng phương thức HTTP, thông thường bao gồm các phương thức xử lý dữ liệu: lấy dữ liệu, chèn dữ liệu, cập nhật dữ liệu hoặc xóa dữ liệu.
Trong REST bao gồm các phương thức:
- POST: Để tạo một tài nguyên trên máy chủ
- GET: Truy xuất tài nguyên
- PUT: cập nhật trạng thái của tài nguyên
- DELETE: Hủy bỏ hoặc xóa một tài nguyên

### b. Phi trạng thái

REST là phi trạng thái, có nghĩa là nó sẽ không lưu giữ thông tin mà người dùng đã bỏ qua trước đó.
- Ví dụ: bạn đang truy cập ở trang thứ 2, bây giờ bạn muốn sang trang thứ 3, REST sẽ không lưu lại thông tin của trang thứ 2 mà bạn đã đi qua. -> REST không quản lý phiên làm việc.

### c. Đưa ra cấu thư mục giống URI

REST đưa ra cấu trúc thư mục  để người dùng có thể dễ dàng truy cập vào tài nguyên thông qua URI,tức nhiên các địa chỉ REST SERVICE cần trực quan, dễ hiểu,dễ đoán đối với người dùng.
- VD: ``` http://myservice.com/weather/vietnam/2016-12-19  ``` : đưa ra thông tin thời tiết của việt nam vào ngày 19-12-2016.

### d. Truyền tải XML,JSON

Thông thường khi một client gửi một yêu cầu tới Webservice hoặc ngược lại, thì thường truyền tải dưới dạng XML hoặc JSON.

## 3. Flask

Flask là một microframework dành cho python, nó dựa trên 2 thư viện chính là Werkzeug và Jinja 2. Flask dễ dàng để sử dụng, nhỏ gọn, nhanh chóng tạo ra một trang web.

### a. Cài đặt Flask

Đầu tiên bạn phải cài đặt Virtualenv.

- Virtualenv là một công cụ hữu ích trong việc tạo ra một môi trường.

khi bạn phát triển nhiều project cùng một lúc với nhiều phiên bản python khác nhau, rất dễ sẽ xảy ra việc chúng không tương thích, hoặc có thể xảy ra mẫu thuẫn. như vậy Virtualenv là giải pháp cho vấn đề này. nó giúp ta có thể cài đặt được nhiều bản python song song với nhau, nó tạo ra các môi trường tương ứng với các project tương ứng, đảm bảo các môi trường là cô lập với nhau.

- cài đặt Virtualenv:

        $sudo pip install virtualenv

    hoặc

        $sudo apt-get install python-virtualenv

Sau khi cài đặt xong Virtualenv, ta cần tạo ra môi trường mới để phát triển:

    $ mkdir myapp
    $ cd myapp
    $ virtualenv venv
    New python executable in venv/bin/python
    Installing setuptools, pip............done.

Như vậy, bất cứ khi nào bạn muốn làm việc, chỉ cần kích môi trường hoạt bằng câu lệnh: `  $ . venv/bin/activate`

Và khi muốn thoát khỏi môi trường, thực hiện câu lệnh: ```$ deactivate```

Sau khi kích hoạt, thực hiện câu lệnh để cài Flask: ```$ pip install flask```

Sau khi cài đặt flask xong, ta cần tạo một file có tên là app.py có nội dung như sau:

```code
from flask import Flask
app=Flask(__name__)

@app.route('/')
def hello():
    return 'hello world!'
if __name__=='__main__':
	app.run()
```

Để chạy chương trình, thực hiện câu lệnh:

```code
$ export FLASK_APP=app.py
$ flask run
```

hoặc thực hiện trực tiếp:

```code
 $ python app.py
 ```
- Đối với các câu lệnh chạy chương trình trên, khi chương trình đang chạy, mà bạn muốn sửa source code, khi đó, việc cập nhật file sẽ không được thực hiện, khi đó chương trình đang chạy vẫn là của file cũ.
để chạy chương trình mới, bạn phải thực hiện khởi động lại chương trình mới bằng tay.
- để thuận tiện cho việc chạy lại chương trình đang chạy mà không cần gõ lại các câu lệnh trên, bạn chỉ cần thêm vào dòng lệnh: `$ export FLASK_DEBUG`

        $ export FLASK_APP=app.py
        $ export FLASK_DEBUG=1
        $ flask run
    Câu lệnh trên giúp việc chương trình tự gỡ lỗi debug và khởi động lại chương trình.

- hoặc sửa câu lệnh `app.run()` thành `app.run(debug=True)` và thực hiện câu lệnh dưới để chạy chương trình :

        $ python init.py


 sau khi chạy thành công, gõ địa chỉ ```http://127.0.0.1:5000/``` và nhận được kết quả là `hello world!`
. Như vậy là đã cài đặt và chạy thành công.

### b. Route

*Route()* được sử dụng để xác định URL, ứng với 1 URL thì sẽ thực hiện 1 function tương ứng, mỗi một route thực hiện một function tương ứng 1 URL nhất định.
Ví dụ:

```code

@app.route('/')
def index():
    return 'Index Page'

@app.route('/hello')
def hello():
    return 'Hello, World'

```
- Ví dụ trên là 2 route, một route có địa chỉ URL là '/' thực hiện function là index(). một route có địa chỉ URL là  '/hello' thực hiện function là hello().
- Route được  định nghĩa  rất tự do, không cần phải cấu hình...
- Nhược điểm của Route là dễ bị phân tán, khó quản lý khi số lượng Route tăng lên.
- trong route ta có thể truyền tham số thông qua địa chỉ URL.

Ví dụ:
```code
@app.route('/user/<username>')
def show_user_profile(username):
    # show the user profile for that user
    return 'User %s' % username
```

- Route trên thực hiện function show_user_profile(usename), với tham số username được truyền vào thông qua địa chỉ URL là: `'/user/<username>'`

### c. HTTP methods

- GET: được sử dụng để nhận thông tin từ SERVER thông qua một địa chỉ URL cung câp.
- POST: được sử dụng để gửi dữ liệu tới Server, dữ liệu có thể là: file, thông tin user, thông tin sản phẩm,....
- HEAD: giống với GET, nhận thông tin từ Server, nhưng HEAD chỉ nhận thông tin phần HTTP header.
- PUT: Cập nhật, chỉnh sửa trạng thái của tài nguyên cho trước thông qua yêu cầu được gửi lên.
- DELETE: hủy bỏ tài nguyên được yêu cầu
- OPTIONS: trả về các phương thức mà Server hỗ trợ

### d. url_for(), render Templates

- **url_for()**: hàm này thực hiện tạo ra một URL với tham số thứ nhất là endpoint, các tham số thứ hai trở đi sẽ được coi là câu truy vấn được nối vào sau ở tham số thứ nhất.

    Ví dụ1: 

        href="{{url_for('static',filename='style.css')}}"
    ví dụ trên tạo ra một URL là đường dẫn tới file `style.css` trong folder là static

    Ví dụ2:

        <p><a href="{{url_for('getcookie')}}">click here</a></p>
    ví dụ trên tạo ra một url khi mà người dùng click vào, nó sẽ được chuyển đến thực hiện một hàm là `getcookie()` trong file chính quản lý các Route.

- Để sử dụng hàm url_for(), ta cần import url_for từ flask `from import Flask,url_for`.

- **Render_template(template_name, *content)**: được sử dụng để trả về tên file template mà có trong folder template, việc cần làm là truyền cho nó 1 tên của template và các biến tham số muốn truyền qua.
    Ví dụ:

        render_template('index.html',name=name)
    Flask sẽ tự động tìm file `index.html` trong folder template, nếu có nó sẽ được thực hiện render ra giao diện tương ứng.


### e. Cookie

Cookie: được sử dụng để duy trì thông tin trạng thái khi bạn vào các trang pages khác nhau trên cùng một website hoặc ghé thăm lại website này tại một thời điểm khác. Cookies cũng có thể giúp bạn lưu lại các mặt hàng bạn đã đặt hàng vào giỏ hàng, lưu thông tin đăng nhập,....
- dữ liệu trong cookie được lưu trữ trên máy client
- ví dụ: sau khi bạn đăng nhập vào một website, cookies giúp bạn duyệt các trang khác nhau trong website mà không cần đăng nhập lại.
- một đối tượng **Request** chứa một thuộc tính cookie. nó là một đối tượng dictionary của tất cả các biến cookie và giá trị tương ứng client truyền đến.
- trong Flask,  cookies được đặt trên response object. Ta có thể sử dụng **make_response()** để nhận một response object từ view, sau đó để lưu trữ một cookie, ta sử dụng hàm **set_cookie()** của response object để lưu trữ. và cuối cùng để đọc 1 cookie, ta sử dụng hàm **get()** (request.cookies) của request để đọc thông qua tên biến truyền vào.

Ví dụ: đầu tiên ta sẽ tạo 1 file `app.py` chứa các phương thức cần thiết:

```sh

    from flask import Flask,render_template,flash, redirect, request,url_for,make_response
    app=Flask(__name__)

    @app.route('/')
    def index():
        return render_template('index.html')

    @app.route('/setcookie',methods=['GET','POST'])
    def setcookie():
        if request.method=='POST':
            user=request.form['name']
            resp= make_response(render_template('readcookie.html'))
            resp.set_cookie('userID',user)
            return resp
    @app.route('/getcookie')
    def getcookie():
        name= request.cookies.get('userID')
        return '<h1>welcome '+name+'</h1>'

    if __name__=='__main__':
        app.run(debug=True)

```

- sau đó tạo một file `index.html` để người dùng nhập đầu vào: 

```html

    <!DOCTYPE html>
    <html>
    <head>
        <title></title>
    </head>
    <body>
        <form action="/setcookie" method="POST">
                <p><h3>Enter userID: </h3></p>
                <p><input type="text" name="name"></p>
                <p><input type="submit" name="login"></p>
        </form>
    </body>
    </html>

```

- tạo 1 file là `readcookie.html` để đọc cookie:

```html

    <!DOCTYPE html>
    <html>
    <head>
        <title></title>
    </head>
    <body>
        <h1>cookie 'UserID' is set</h1>
        <p><a href="{{url_for('getcookie')}}">click here to read cookie</a></p>

    </body>
    </html>

```
- Ví dụ trên được mô tả như sau: sau khi chạy chương trình người dùng sẽ thực hiện nhập input, sau đó nhấn submit -> được chuyển tới hàm `setcookie()`, hàm `setcookie()` thực hiện nhần request từ `index.html` xử lý và lưu giá trị vào cookie, rồi thực hiện chuyển sang file `readcookie.html`, khi đó người dùng sẽ click và link `click here`, sau đó được chuyển tới hàm `getcookie()`, hàm này thực hiện đọc dữ liệu trong cookie, sau đó trả về kết quả.

### f. Session

-không giống như cookie, dữ liệu trong Session được lưu trữ trên Server, thời gian sống của Session là từ khi client **log in** cho tới khi client thực hiện **log out**.
- **Session** là một object của Flask, cho phép bạn lưu thông tin của người dùng khi họ truy cập vào ứng dụng. Session mã hóa cookies, cho phép người dùng có thể nhìn nhưng không thể chỉnh sửa cookies, trừ khi người dùng biết được khóa bảo mật được dùng để mã hóa, để mã hóa, Flask định nghĩa một **SECRET_KEY**. **SECRET_KEY** có thể là một chuỗi ngẫu nhiên do bạn từ định nghĩa.
- một **SECRET_KEY** càng an toàn thì càng phải mang tính ngẫu nhiên. để có thể sinh một chuỗi ngẫu nhiên, bạn có thể sử dụng một hàm là **os.urandom()**.

```python

    >>> import os
    >>> os.urandom(24)
    kq: 'R\x1a\x1b\xba!\xdb\xd7\xe1nO\xc7\x18$\x97\xa1+H\xbf>2\xfa\x96\xc9\x1d'

```
- Để thực hiện lưu giá trị vào session, ta sử dụng câu lệnh:

        sesion['ten']= gia_tri
    Ví dụ:
        session['name']= 'admin'
- Để thực hiện hủy giá trị được lưu trong session, ta sử dụng câu lệnh: 

        session.pop('key',default)

nếu **key** có trong session, hủy nó và trả về giá trị của **key**, nếu không giá trị **default** được trả về. nếu `default` không được đưa ra và `key` là không có trong session, một lỗi **KeyError** sẽ được đưa ra.

    Ví dụ:

        session.pop('name',None)

- Ví dụ về Session:
```python

    from flask import Flask, session, redirect, url_for, escape, request

    app = Flask(__name__)

    @app.route('/')
    def index():
        if 'username' in session:
            return 'Logged in as %s' % escape(session['username'])
        return 'You are not logged in'

    @app.route('/login', methods=['GET', 'POST'])
    def login():
        if request.method == 'POST':
            session['username'] = request.form['username']
            return redirect(url_for('index'))
        return '''
            <form method="post">
                <p><input type=text name=username>
                <p><input type=submit value=Login>
            </form>
        '''

    @app.route('/logout')
    def logout():
        # remove the username from the session if it's there
        session.pop('username', None)
        return redirect(url_for('index'))

    # set the secret key.  keep this really secret:
    app.secret_key = 'A0Zr98j/3yX R~XHH!jmN]LWX/,?RT'

```

### g. Response

- Giá trị trả về của 1 hàm sẽ được tự động convert sang response object(thường ở dạng Json).
- nếu giá trị trả về là String, nó sẽ tự động convert thành response object.
- nếu giá trị trả về thuộc kiểu tuple, thì giá trị tuple phải ở dạng (response,status,headers) hoặc (response,headers), với status có thể là một String hoặc một Integer, headers có thể là một list hoặc một dictionary.


## 4. sử dụng Curl để thử nghiệm các Request

Curl là một công cụ được sử dụng để gửi dữ liệu từ server hoặc tới một server, nó hỗ trợ hầu hết các giao thức như: DICT,FILE,FTP,FPTS,HTTP,HTTPS,... curl  được sử dụng mà không cần sự tương tác của người dùng.

Curl hỗ trợ các phương thức của HTTP: GET,POST, DELETE,PUT...

Dưới đây là cách sử dụng curl đối với các phương thức của HTTP

- Để sử dụng các phương thức của HTTP, ta có thể sử dụng câu lệnh:

        $ curl -X Y URL

- Trong đó:

    + Y có thể là phương thức: POST, GET, HEAD, PUT,..

    + url là địa chỉ muốn gửi yêu cầu tới.

    + -X :  được hiểu là cho biết phương thức nào sẽ được sử dụng.

**GET**: được sử dụng để truy xuất tài nguyên từ server thông qua request từ client. client gửi một yêu cầu tới server và nhận dữ liệu từ yêu cầu đó.

Để thực hiện, ta sử dụng câu lệnh: `$ curl URL`
. TRrong đó, URL là địa chỉ mà ta muốn truy cập tới.
- Ví dụ:

        $ curl http://127.0.0.1:5000/infor

- Với câu lệnh trên, phương thức mặc định được sử dụng là phương thức GET

**POST**: Được sử dụng để gửi dữ liệu lên máy chủ, để thực hiện POST ta sử dụng câu lệnh:

        $ curl -X POST -d 'data' URL

- Đối với câu lệnh trên, ta chỉ rõ POST là phương thức được sử dụng.

    hoặc sử dụng `--data` khi đó phương thức được sử dụng mặc định sẽ là POST:

        $ curl --data 'data' URL

+ Ví dụ:

         $ curl --data 'usename=dan&password=123' http://127.0.0.1:5000/create

Ngoài ra còn có một số lựa chọn như: 
- -i : yêu cầu in ra cả vùng header của gói tin phản hồi.
    VD:

        $ curl -i http://127.0.0.1:5000/
- -H: được dùng để thiết lập các thông tin cho phần header.

    Ví dụ:

        $ curl -H "Content-Type: application/json" http://127.0.0.1:5000/index
        $ curl -H "Host: www.example.com" -H "Accept-language:en" URL

- --form: được sử dụng để upload file từ client lên server.
        VD:

        $ curl --form "fileupload=../path/myfile.txt"
    Câu lệnh trên sẽ upload file từ địa địa chỉ `../path/myfile.txt` lên server tại địa chỉ URL: `http://127.0.0.1:5000/uploadfile`

- -O : được dùng để tải một tập tin trên web về máy.

    Ví dụ:

        $ curl -O https://example.com/downloads/file.zip

    Câu lệnh trên được sử dụng để tải tập tin `file.zip` trên địa chỉ `https://example.com/downloads/file.zip` về thư mục hiện tại trên máy.
    hoặc sử dụng câu lệnh sau để đổi tên tập tin mà chúng ta tải về từ `file.zip` thành `my_file.zip`:

        $ curl -O my_file.zip http://example.com/downloads/file.zip
