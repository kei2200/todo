<script setup>
  import {ref} from 'vue';
  //Vueの機能の一つであるrefをインポートしています。
  //refは、Vueが提供するリアクティブな変数を定義するための関数です。
  const todoRef = ref('');
  //todoRefという変数を定義し、その初期値を空文字列に設定しています。
  //ref()で新しいリアクティブ変数を作成し、その変数の初期値を引数で指定することができます。
  //todoRefは、後でTODOのテキスト入力欄にバインドされます。
  const todoListRef = ref([]);
  //todoListRefという変数を定義し、その初期値を空の配列に設定しています。todoListRefは、
  //TODOアイテムを格納するためのリストとして使用されます。

  const ls = localStorage.todoList;
  //localStorage.todoListの値を取得し、変数lsに代入しています。
  //localStorageは、Webブラウザにデータを保存するオブジェクトであり、
  //localStorage.todoListは、キーがtodoListのローカルストレージの値を表します。
  //もしローカルストレージにtodoListが存在する場合は、JSON.parseを使ってその値をパースして、
  //配列を復元し、todoListRef.valueに代入します。
  
  todoListRef.value = ls ? JSON.parse(ls) : [];
  //todoListRefは、refで作成されたリアクティブ変数であり、そのvalueプロパティにアクセスすることで、
  //その変数の値にアクセスできます。このコードでは、todoListRef.valueに、現在のTODOリストの配列を代入しています。

  const addTodo = () =>{
    //アロー関数。変数に直接関数を代入している。無名関数とも。
    //ボタン部分の@clickに同様の変数を入れているからボタンをクリックすると代入された関数が走る
 
    const id = new Date().getTime();
    //変数IDに現在の時間を取得して代入している 

    todoListRef.value.push({
      id: id,
      task: todoRef.value

      //pushメソッドは、配列の末尾に新しい要素を追加します。
      //このコードでは、新しいTODOアイテムを配列に追加するために、todoListRef.value.pushを使っています。
      //この新しいTODOアイテムは、オブジェクトとして表され、idとtaskという2つのプロパティを持っています。
      //idは、新しいTODOアイテムの一意のIDを表し、taskは、TODOアイテムのテキストを表します。
      //また、このコードでは、ローカルストレージにTODOリストを保存するために、JSON.stringifyを使って、
      //todoListRef.valueの内容をJSON形式の文字列に変換しています。

    });

    localStorage.todoList = JSON.stringify(todoListRef.value);
    //localStorage.todoListというキーに、TODOリストの内容をJSON形式の文字列に変換したものを代入しています。
    //JSON.stringifyは、JavaScriptオブジェクトをJSON形式の文字列に変換するメソッドです。
    //JSON.stringify(todoListRef.value)は、todoListRef.valueの内容をJSON形式の文字列に変換します。
    todoRef.value ='';
    //todoRef.value ='';は、TODOのテキスト入力欄をリセットするためのコードです。
    //todoRefは、refで作成されたリアクティブ変数であり、valueプロパティでその値にアクセスできます。
    //todoRef.valueに空文字列を代入することで、テキスト入力欄の内容を空にすることができます。
  }
</script>

<template>
  <div class="box__input">
    <input
      type="text"
      class="todo__input"
      v-model="todoRef"
      placeholder="+TODOを入力"
    />
    <button class="btn" @click="addTodo">追加</button>
  </div>
  <div class="box__list">
    <div class="todo__list" v-for="todo in todoListRef" :key="todo.id">
      <div class="todo">
        <input type="checkbox" class="check"/>
        <label>{{ todo.task }}</label>
      </div>
      <div class="btns">
        <button class="btn green">編</button>
        <button class="btn pink">削</button>
      </div>
    </div>
  </div>
</template>

<style scoped>
    .box__input {
        margin-top: 20px;
        display: flex;
    }
    .todo__input{
        width: 300px;
        margin-right: 8px;
        padding: 8px;
        font-size: 18px;
        border: 1px solid #aaa;
        border-radius: 6px;
    }
    .btn{
        padding: 8px;
        background-color: #03a9f4;
        border-radius: 6px;
        color: #fff;
        text-align: center;
        font-size: 14px;
        white-space: nowrap;
        border: none;
    }
    .box__list{
      margin-top: 20px;
      display: flex;
      flex-direction: column;
      gap:4px;
    }
    .todo__list{
      display: flex;
      align-items: center;
      gap: 8px;
    }
    .todo{
      border: 1px solid #ccc;
      border-radius: 6px;
      padding: 12px;
      width: 300px;
    }
    .check{
      border: 1px solid red;
      transform: scale(1.6);
      margin: 0 16px 2px 6px;
    }
    .btns{
      display: flex;
      gap: 4px;
    }
    .green{
      background-color: #00c853;
    }
    .pink{
      background-color: #ff4081;
    }
</style>
