<script setup>
  import {ref} from 'vue'; //Vueの機能の一つであるrefをインポートしています。refは、Vueが提供するリアクティブな変数を定義するための関数です。
  const todoRef = ref('');//todoRefという変数を定義し、その初期値を空文字列に設定しています。ref()で新しいリアクティブ変数を作成し、その変数の初期値を引数で指定することができます。todoRefは、後でTODOのテキスト入力欄にバインドされます。
  const todoListRef = ref([]);//todoListRefという変数を定義し、その初期値を空の配列に設定しています。todoListRefは、TODOアイテムを格納するためのリストとして使用されます。
  const addTodo = () =>{//アロー関数。変数に直接関数を代入している。無名関数とも。ボタン部分の@clickに同様の変数を入れているからボタンをクリックすると代入された関数が走る
    const id = new Date().getTime();//変数IDに現在の時間を取得して代入している 
    todoListRef.value.push({//todoListRefは、空の配列を参照するリアクティブ変数です。pushメソッドを使って、配列に新しい要素を追加しています。追加する要素は、オブジェクトです。このオブジェクトには、idとtaskという2つのプロパティがあります。idは、現在の時間（ミリ秒単位）を表す数字であり、ユニークな識別子として使用されます。taskは、ユーザーが入力したTODOの内容です。新しい要素を配列に追加することで、TODOリストの内容が更新されます。この変更に伴って、画面の表示も更新されます。todoListRef.valueが変更されると、Vueは自動的に再描画を行い、最新のTODOリストの内容が画面に反映されます。
      id: id,
      task: todoRef.value
    });
    localStorage.todoList = JSON.stringify(todoListRef.value);
    //localStorage.todoListというキーに、TODOリストの内容をJSON形式の文字列に変換したものを代入しています。JSON.stringifyは、JavaScriptオブジェクトをJSON形式の文字列に変換するメソッドです。JSON.stringify(todoListRef.value)は、todoListRef.valueの内容をJSON形式の文字列に変換します。
    todoRef.value ='';
    //todoRef.value ='';は、TODOのテキスト入力欄をリセットするためのコードです。todoRefは、refで作成されたリアクティブ変数であり、valueプロパティでその値にアクセスできます。todoRef.valueに空文字列を代入することで、テキスト入力欄の内容を空にすることができます。
  }
</script>

<template>
  <div class="box__input">
    <input type="text" class="todo__input" v-model="todoRef" placeholder="+TODOを入力">
    <button class="btn" @click="addTodo">追加</button>
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
</style>
