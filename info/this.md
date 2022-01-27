# `this`

✅ 자바스크립트에서 모든 함수는 실행될 때마다 함수 내부에 this라는 객체가 추가됩니다.
✅ this는 함수가 호출되는 상황에 따라서 달라집니다.

1.  객체의 메서드를 호출할 때
    객체의 프로퍼티가 함수일 경우에는 메서드라고 합니다.

    ```
    var myObject = {
        name: "foo",
        sayName: function() {
        console.log(this); // 여기서 this는 myObject를 참조
        }
    };

    myObject.sayName();
    console> Object {name: "foo", sayName: sayName()}
    ```

    ➡️ 메서드에서 this 는 메서드를 포함하고 있는 객체를 참조합니다. (해당 메서드를 호출한 객체가 바인딩 되는 것)

2.  함수를 호출할 때
    ✅ 객체의 메서드가 아니라 함수를 호출하면 this 는 전역 객체에 바인딩됩니다.

    ```
    var value = 100;
    var myObj = {
        value: 1,
        func1: function() {
            console.log(`func1's this.value: ${this.value}`);

            var func2 = function() {
                 console.log(`func2's this.value ${this.value}`);
            };
        func2();
        }
    };

    myObj.func1();
    console> func1's this.value: 1
    console> func2's this.value: 100
    ```

- func1 은 myObj 객체의 메서드이기 때문에 this에는 myObj가 바인딩 된다.
- func2는 메서드가 아닌 함수이기 때문에 this에는 전역 객체가 바인딩된다.

3. 생성자 함수를 통해 객체를 생성할 때
   ✅ new 키워드를 통해서 생성자 함수를 호출할 때는 this는 인스턴스가 됩니다.
   ✅ new를 사용하면 빈 객체가 생성되는 것입니다.

   ```
   let Person = function (name, year, job) {
     this.name = name;
     this.year = year;
     this.job = job;
     console.log(this);
   };

   var john = new Person("hi", 1996, "hoho"); // new 를 통해서 새로운 빈 object 가 생성된 것이다. 그리고john 에 할당해주는 것이다.


    var Person = function(name) {
        console.log(this);
        this.name = name;
    };

    var foo = new Person("foo"); // Person
    console.log(foo.name); // foo
   ```

4. apply, call, bind를 통한 호출
   ➡️ bind 는 함수가 가리키는 this 만 바꾸고 호출하지 않음. (this 를 고정시킨다)
   ➡️ call 은 this를 바인딩하고 함수를 호출하고 실행시킨다. (this 를 설정해줄 수 있다)
   ➡️ apply 는 call과 거의 똑같지만 인자 전달을 배열로 해준다.

   ```
   var john = {
    name: "heeje",
    age: 25,
    job: "student",
    presentation: function (style, day) {
      if (style === "formal") {
        console.log(
         "good moring" + day + "i'm " + this.name + this.job + this.age
        );
      } else if (style === "friendly") {
     console.log("hey what's up?" + this.name + this.job + this.age);
        }
      },
    };


    john.presentation("formal", "morning");

    var jane = {
      name: "jane",
      age: 25,
      job: "pro",
    };
   ```

john.presentation.call(jane, "friendly", "afternoon"); // call method (jane 을 전달. this를 바인딩 )

// => john.presentation.apply(jane, ["friendly", "afternoon"]);

let johnFriendy = john.presentation.bind(jane); //bind method -> this를 jane 으로 변경 -> 함수를 실행하지 않는다.
johnFriendy("friendly", "moring");
