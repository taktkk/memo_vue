<script setup>
import { ref } from 'vue'

      let name = ref('');
      let zip = ref('');
      let prefecture = ref('');
      let address = ref('');
      let building = ref('');
      let interests = ref([]);
      const interestsMaxCount = ref(3);
      // let errors = ref({
      //   name: [],
      //   zip: [],
      //   prefecture: [],
      //   address: [],
      //   interests: []
      // });
    
    
      const zipToAddress = () => {
        var self = this;
        new YubinBango.Core(this.zip, function (addr) {
          if (addr.region_id) {
            self.prefecture = addr.region;
            self.address = addr.locality + addr.street;
          } else {
            self.errors.zip.push('該当する住所がありません');
          }
        });
      };
      const addInterests = () => {
        this.interests.push('');
      };
      const removeInterests = (index) => {
        this.interests.splice(index, 1);
      };
      const validate = () => {
        var errors = {
          name: [],
          zip: [],
          prefecture: [],
          address: [],
          interests: []
        };
        if (!this.name) {
          errors.name.push('必須項目が入力されていません');
        } else if(this.name.length > 20) {
          errors.name.push('20文字以内で入力してください。');
        }
        if (!this.zip) {
          errors.zip.push('必須項目が入力されていません');
        } else {
          if (!this.zip.match(/\d{3}-?\d{4}/)) {
            errors.zip.push('書式が正しくありません');
          }
        }
        if (!this.prefecture) {
          errors.prefecture.push('必須項目が入力されていません');
        }
        if (!this.address) {
          errors.address.push('必須項目が入力されていません');
        } else if(this.address.length > 40) {
          errors.address.push('40文字以内で入力してください。');
        }
        if (this.interests.length <= 1 && !this.interests[0]) {
          errors.interests.push('必須項目が入力されていません');
        }
        this.errors = errors;
      };
   
    
      const canAddInterests = () => {
        return this.interests.length < this.interestsMaxCount;
      };
      const canRemoveInterests = () => {
        return this.interests.length > 1;
      }
    
</script>

  
<template>
  <main class="main">
    <section class="block">
      <h1 class="block-title">お問い合わせ</h1>
      <div class="block-body">
        <form action="" class="form">
          <fieldset>
            <div class="form-group">
              <label for="name">お名前<span class="badge">必須</span></label>
              <input type="text" name="name" id="name" v-model="name">
              <div class="errors" v-if="errors">
                <div class="error" v-for="error in errors">{{ error }}</div>
              </div>
            </div>

            <div class="form-group">
              <label for="zip">郵便番号<span class="badge">必須</span></label>
              <div class="form-row">
                <input type="text" name="zip" id="zip" v-model="zip" placeholder="101-0064">
                <button class="button-outline" @click.prevent="zipToAddress">住所を入力</button>
              </div>
              <div class="errors" v-if="errors">
                <div class="error" v-for="error in errors">{{ error }}</div>
              </div>
            </div>

            <div class="form-group">
              <label for="prefecture">都道府県<span class="badge">必須</span></label>
              <select name="prefecture" id="prefecture" v-model="prefecture">
                <option value="">選択してください</option>
                <option value="北海道">北海道</option>
                <option value="青森県">青森県</option>
                <option value="岩手県">岩手県</option>
                <option value="宮城県">宮城県</option>
                <option value="秋田県">秋田県</option>
                <option value="山形県">山形県</option>
                <option value="福島県">福島県</option>
                <option value="茨城県">茨城県</option>
                <option value="栃木県">栃木県</option>
                <option value="群馬県">群馬県</option>
                <option value="埼玉県">埼玉県</option>
                <option value="千葉県">千葉県</option>
                <option value="東京都">東京都</option>
                <option value="神奈川県">神奈川県</option>
                <option value="新潟県">新潟県</option>
                <option value="富山県">富山県</option>
                <option value="石川県">石川県</option>
                <option value="福井県">福井県</option>
                <option value="山梨県">山梨県</option>
                <option value="長野県">長野県</option>
                <option value="岐阜県">岐阜県</option>
                <option value="静岡県">静岡県</option>
                <option value="愛知県">愛知県</option>
                <option value="三重県">三重県</option>
                <option value="滋賀県">滋賀県</option>
                <option value="京都府">京都府</option>
                <option value="大阪府">大阪府</option>
                <option value="兵庫県">兵庫県</option>
                <option value="奈良県">奈良県</option>
                <option value="和歌山県">和歌山県</option>
                <option value="鳥取県">鳥取県</option>
                <option value="島根県">島根県</option>
                <option value="岡山県">岡山県</option>
                <option value="広島県">広島県</option>
                <option value="山口県">山口県</option>
                <option value="徳島県">徳島県</option>
                <option value="香川県">香川県</option>
                <option value="愛媛県">愛媛県</option>
                <option value="高知県">高知県</option>
                <option value="福岡県">福岡県</option>
                <option value="佐賀県">佐賀県</option>
                <option value="長崎県">長崎県</option>
                <option value="熊本県">熊本県</option>
                <option value="大分県">大分県</option>
                <option value="宮崎県">宮崎県</option>
                <option value="鹿児島県">鹿児島県</option>
                <option value="沖縄県">沖縄県</option>
              </select>
              <div class="errors" v-if="errors">
                <div class="error" v-for="error in errors">{{ error }}</div>
              </div>
            </div>

            <div class="form-group">
              <label for="address">市区町村・番地<span class="badge">必須</span></label>
              <input type="text" name="address" id="address" v-model="address" placeholder="千代田区神田錦町3-1">
              <div class="errors" v-if="errors">
                <div class="error" v-for="error in errors">{{ error }}</div>
              </div>
            </div>

            <div class="form-group">
              <label for="building">ビル名等</label>
              <input type="text" name="building" id="building" v-model="building" placeholder="〇〇ビル 7F">
            </div>

            <div class="form-group">
              <label>興味のある分野（最大3つまで）<span class="badge">必須</span></label>
              <div class="form-row" v-for="(interest, index) in interests">
                <input type="text" :name="'interest' + index" v-model="interests[index]">
                <button class="button-outline" v-if="canRemoveInterests" @click.prevent="removeInterests(index)">削除</button>
              </div>
              <div class="errors" v-if="errors">
                <div class="error" v-for="error in errors">{{ error }}</div>
              </div>
              <button class="button-outline" v-if="canAddInterests" @click.prevent="addInterests">追加</button>
            </div>

            <p>
              <input class="button" type="submit" value="送信する" @click.prevent="validate">
            </p>
          </fieldset>
        </form>
      </div>
    </section>
  </main>
</template>

<style scoped>
    form {
      width: 50%;
      margin: 0 auto;
    }
    .form-row {
      display: flex;
      margin-top: 2px;
    }
    .form-row button {
      flex: auto;
      margin-left: 10px;
    }
    .badge {
      font-size: 10px;
      font-weight: bold;
      line-height: 1;
      display: inline-block;
      background: #f36565;
      color: #fdfdfd;
      padding: 4px 8px;
      border-radius: 2px;
      margin-left: .5em;
      position: relative;
      top: -1px;
    }
    .errors {
      color: red;
      margin: 10px 0 0;
      font-size: 12px;
    }
    * {
  box-sizing: border-box;
}
body {
  background: #83fad2;
  padding: 40px 0;
  color: #555;
  -webkit-font-smoothing: antialiased;
  font-smoothing: antialiased;
}
.main {
}

.block {
  background: #fff;
  width: 550px;
  margin: 0 auto;
  border-radius: 40px;
  box-shadow: 0 0 40px rgba(0,0,0,0.2);
  overflow: hidden;
}
.block-title {
  text-align: center;
  margin: 0;
  padding: 30px 0;
  background: #f6f7fa;
  color: #555;
  font-weight: bold;
  font-size: 20px;
  line-height: 1;
}
.block-body {
  padding: 30px 50px;
}

.button {
  background: #83fad2;
  color: #fff;
  font-size: 14px;
  font-weight: bold;
  display: block;
  width: 100%;
  padding: 15px;
  border: none;
  cursor: pointer;
  border-radius: 20px;
  outline: none;
}
.button-outline {
  background: #fff;
  color: #83fad2;
  border: 1px solid #83fad2;
  border-radius: 10px;
  font-size: 12px;
  font-weight: bold;
  display: inline-block;
  padding: 0 10px;
  min-width: 8em;
  cursor: pointer;
  outline: none;
  transition: .2s;
}
.button-outline:hover {
  background-color: #83fad2;
  color: #fff;
}

.form {
  width: 100%;
}
fieldset {
  border: none;
  padding: 0;
  margin: 0;
}
label {
  display: block;
  font-size: 14px;
  margin: 0 0 10px;
}
input[type="text"],
input[type="email"] {
  border: 1px solid #eee;
  border-radius: 5px;
  font-size: 14px;
  display: block;
  width: 100%;
  padding: 10px;
  outline: none;
  transition: 0.2s;
}
input::placeholder {
  color: #ccc;
}
input:focus {
  border-color: #83fad2;
  box-shadow: 0 4px 10px rgba(0,0,0,0.02);
}
select {
  border: 1px solid #eee;
  border-radius: 5px;
  background: #fff;
  font-size: 14px;
  display: block;
  width: 100%;
  padding: 10px;
  height: 38px;
}
.form-group {
  margin: 0 0 30px;
}
  </style>