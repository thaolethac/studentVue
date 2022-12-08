<template>
  <div class="container">
    <form>
      <input
        type="text"
        placeholder="Từ khóa cần tìm..."
        style="border: 3px solid red; height: 35px"
        @keyup="(e) => myFunctionSearch(e.target.value)"
        id="myInput"
      />
      <button class="button-search" @click.stop.prevent="button">
        Tìm kiếm
      </button>
    </form>
    <div class="update-form">
      <table style="width: auto; height: 100px">
        <tr>
          <th>Mã SV<span class="span-requried">(*)</span></th>
          <th>Tên Sinh Viên<span class="span-requried">(*)</span></th>
          <th>Ngày sinh</th>
          <th>Giới tính</th>
          <th>Khoa<span class="span-requried">(*)</span></th>
        </tr>
        <tr>
          <td>
            <input
              type="text"
              class="update"
              ref="inputMsv"
              required
              :value="Msv"
              @change="(e) => (this.Msv = e.target.value)"
              id="add1"
            />
          </td>
          <td>
            <input
              type="text"
              class="update"
              required
              :value="Tensv"
              @change="(e) => (this.Tensv = e.target.value)"
              id="add2"
            />
          </td>
          <td>
            <input
              type="text"
              class="update"
              :value="Ngaysinh"
              @change="(e) => (this.Ngaysinh = e.target.value)"
              id="add3"
            />
          </td>
          <td>
            <form class="form-general">
              <input
                ref="input1"
                type="radio"
                value="Nam"
                name="gioitinh"
                id="add4"
                @click="(e) => (this.Gioitinh = e.target.value)"
              />
              <label for="nam">Nam</label><br />
              <input
                ref="input2"
                type="radio"
                value="Nữ"
                name="gioitinh"
                id="add5"
                @click="(e) => (this.Gioitinh = e.target.value)"
              />
              <label for="nu">Nữ</label>
            </form>
          </td>
          <td>
            <input
              type="text"
              class="update"
              :value="Khoa"
              required
              @change="(e) => (this.Khoa = e.target.value)"
              id="add6"
            />
          </td>
          <td class="button">
            <button id="addsv" ref="updatebutton" @click="addsvv">
              Thêm mới
            </button>
          </td>
          <td>
            <button @click="update">Cập nhật</button>
          </td>
          <td>
            <button id="add" @click="delinput">Xóa</button>
          </td>
        </tr>
      </table>
    </div>
  </div>
  <div class="container-table">
    <table id="addtable" class="list-tr" style="width: 800px">
      <tr>
        <th>&emsp;&emsp;&emsp;</th>
        <th>Mã SV</th>
        <th>Tên Sinh Viên</th>
        <th>Ngày sinh <span class="span-requried">(*)</span></th>
        <th>Giới tính</th>
        <th>Khoa <span class="span-requried">(*)</span></th>
        <th>Sửa</th>
        <th>Xóa</th>
      </tr>
      <tr v-for="student in Students" :key="student.Msv">
        <td>
          <input type="checkbox" />
        </td>
        <td>{{ student.Msv }}</td>
        <td>{{ student.Tensv }}</td>
        <td>{{ student.Ngaysinh }}</td>
        <td>{{ student.Gioitinh }}</td>
        <td>{{ student.Khoa }}</td>
        <td>
          <button @click="Edit(student.Msv)">Sửa</button>
        </td>
        <td>
          <button @click="Delete(student.Msv)">Xóa</button>
        </td>
      </tr>
    </table>
    <!-- <button onclick="del()" id="del">Xóa</button> -->
  </div>
</template>

<script>
import { reactive, ref } from "vue";
const input1 = ref(null);
const input2 = ref(null);
const inputMsv = ref(null);
const array = ref([]);
const updatebutton = ref(null);

export default {
  name: "ShowStudent",
  setup() {
    const state = reactive({ count: 0 });

    // expose the state to the template
    return {
      state,
      input1,
      input2,
      inputMsv,
      array,
      updatebutton,
    };
  },
  data() {
    return {
      Students: [
        {
          Msv: 21000645,
          Tensv: "Lê Thạc Thao",
          Ngaysinh: "05/09/2003",
          Gioitinh: "Nữ",
          Khoa: "Kiểm toán viên",
        },
        {
          Msv: 21000642,
          Tensv: "Lê Thạc Thao",
          Ngaysinh: "05/09/2003",
          Gioitinh: "Nữ",
          Khoa: "Kiểm toán viên",
        },
        {
          Msv: 21000245,
          Tensv: "Le Cha Zoo",
          Ngaysinh: "05/09/2003",
          Gioitinh: "Nữ",
          Khoa: "Kiểm toán viên",
        },
        {
          Msv: 21000455,
          Tensv: "Lee Min Ho",
          Ngaysinh: "05/09/2003",
          Gioitinh: "Nam",
          Khoa: "Diễn viên",
        },
        {
          Msv: 21000102,
          Tensv: "Lee Min Ho",
          Ngaysinh: "05/09/2003",
          Gioitinh: "Nam",
          Khoa: "Diễn viên",
        },
        {
          Msv: 123,
          Tensv: "Lee Min Ho",
          Ngaysinh: "05/09/2003",
          Gioitinh: "Nam",
          Khoa: "Diễn viên",
        },
        {
          Msv: 21000655,
          Tensv: "Lee Min Ho",
          Ngaysinh: "05/09/2003",
          Gioitinh: "Nam",
          Khoa: "Diễn viên",
        },
        {
          Msv: 21000365,
          Tensv: "Lee Min Ho",
          Ngaysinh: "05/09/2003",
          Gioitinh: "Nam",
          Khoa: "Diễn viên",
        },
        {
          Msv: 21000789,
          Tensv: "Lee Min Ho",
          Ngaysinh: "05/09/2003",
          Gioitinh: "Nam",
          Khoa: "Diễn viên",
        },
        {
          Msv: 21000546,
          Tensv: "Lee Min Ho",
          Ngaysinh: "05/09/2003",
          Gioitinh: "Nam",
          Khoa: "Diễn viên",
        },
      ],

      Msv: " ",
      Tensv: " ",
      Ngaysinh: " ",
      Gioitinh: " ",
      Khoa: " ",
      show: false,
    };
  },
  methods: {
    Delete(x) {
      this.Students.forEach((e, index) => {
        if (e.Msv.toString() === x.toString()) {
          this.Students.splice(index, index + 1);
        }
      });
      console.log(this.Students[0]);
    },
    Edit(x) {
      this.Students.forEach((e) => {
        if (e.Msv.toString() === x.toString()) {
          this.Msv = parseInt(e.Msv);
          this.Tensv = e.Tensv;
          this.Ngaysinh = e.Ngaysinh;
          this.Khoa = e.Khoa;
          if (e.Gioitinh === "Nam") {
            input1.value.checked = true;
            this.Gioitinh = "Nam";
          } else {
            input2.value.checked = true;
            this.Gioitinh = "Nữ";
          }
        }
      });
      inputMsv.value.disabled = true;
      updatebutton.value.disabled = true;

      console.log(inputMsv);
      return [this.Msv, this.Tensv, this.Ngaysinh, this.Gioitinh, this.Khoa];
    },
    button() {
      // console.log(tr[0].Msv);
    },
    // onChange(e) {
    //   this.Msv = e;
    //   this.Tensv = e;
    //   console.log(this.Msv);
    // },
    update() {
      const msv = inputMsv.value.value;
      if (msv === " ") {
        alert("Không có gì để cập nhật!!!");
      }
      this.Students.forEach((e, index) => {
        if (e.Msv.toString() === msv.toString()) {
          this.Students[index].Tensv = this.Tensv;
          this.Students[index].Ngaysinh = this.Ngaysinh;
          this.Students[index].Gioitinh = this.Gioitinh;
          this.Students[index].Khoa = this.Khoa;
        }
      });
      console.log(this.Edit(msv)[1]);
      inputMsv.value.disabled = false;
      updatebutton.value.disabled = false;
    },
    check() {
      for (let i = 0; i < this.Students.length; i++) {
        if (this.Students[i].Msv.toString() === this.Msv.toString()) {
          return false;
        }
        return true;
      }
    },
    addsvv() {
      if (this.Msv === " ") {
        alert("Mời bạn nhập mã Sinh Viên");
      } else if (this.Tensv === " ") {
        alert("Mời bạn nhập tên Sinh viên");
      } else if (this.Ngaysinh === " ") {
        alert("Mời bạn nhập ngày sinh của Sinh Viên");
      } else if (this.Gioitinh === " ") {
        alert("Mời bạn nhập giới tính của Sinh Viên");
      } else if (this.Khoa === " ") {
        alert("Mời bạn nhập khoa của Sinh Viên");
      } else {
        if (!this.check()) {
          this.Students.push({
            Msv: parseInt(this.Msv),
            Tensv: this.Tensv,
            Ngaysinh: this.Ngaysinh,
            Gioitinh: this.Gioitinh,
            Khoa: this.Khoa,
          });
        } else {
          alert("Bạn đã nhập trùng mã sinh viên");
        }
      }
      console.log(this.check());
      // input.value.value = " ";
      input1.value.checked = false;
      input2.value.checked = false;
      this.Msv = " ";
      this.Tensv = " ";
      this.Ngaysinh = " ";
      this.Gioitinh = " ";
      this.Khoa = " ";
    },
    delinput() {
      input1.value.checked = false;
      input2.value.checked = false;
      this.Msv = " ";
      this.Tensv = " ";
      this.Ngaysinh = " ";
      this.Gioitinh = " ";
      this.Khoa = " ";
      inputMsv.value.disabled = false;
      updatebutton.value.disabled = false;
    },
    myFunctionSearch(x) {
      var table = document.getElementById("addtable");
      var tr = table.getElementsByTagName("tr");
      console.log(x);
      for (let i = 0; i < this.Students.length; i++) {
        if (this.Students[i].Msv.toString().toUpperCase().indexOf(x) > -1) {
          // console.log(tr[i + 1]);
          tr[i + 1].style.display = "";
        } else {
          tr[i + 1].style.display = "none";
        }
      }
    },
  },
  // module.exports = {
  // };
};
</script>

<style scoped>
* {
  box-sizing: borderBox;
  padding: 5px;
  margin: 0;
  font-family: "Trebuchet MS", "Lucida Sans Unicode", "Lucida Grande",
    "Lucida Sans", Arial, sans-serif;
}
table {
  border-collapse: collapse;
  text-align: center;
}
table,
td,
th {
  border: 1px solid #333;
}
td,
th {
  padding: 7px;
}
th {
  background-color: #04aa6d;
}
button {
  padding: 5px;
  margin-left: 2px;
}
form {
  padding: 10px;
}
label {
  font-weight: bold;
}
.form-1 input {
  padding: 5px 5px 5px 1px;
  font-size: 14px;
  margin: 0px 0px 0px 5px;
  margin-top: 1px;
}
.table-1 {
  marginbottom: 100px;
  border-radius: 10px;
}
.table-1 td,
.table-1 th {
  width: 100px;
}
.table-1 input {
  font-size: 16px;
  padding: 2px;
}
input {
  border: 2px solid #333;
  border-radius: 6px;
}

.form-1 {
  margin-left: -10px;
}
.form-general input {
  /* display: block; */
  float: left;
}
.form-general label {
  margin-top: -5px;
}
.button-search {
  background-color: red;
  color: #fff;
  font-size: 15px;
  /* padding: 2px; */
  border-radius: 5px;
}
</style>
