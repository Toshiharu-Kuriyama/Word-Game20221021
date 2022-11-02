#include <iostream>
#include <string>
#include <vector>
#include <cctype>
#include <algorithm>
using namespace std;

int main() {
  vector<string> nameInventory;//プレイヤーの名前を格納する配列
  vector<string> wordInventory;//文字を格納する配列
  wordInventory.push_back("shiritori");
  string name;//プレイヤーの名前
  string word;//入力された文字
  string lastWard;//前回の文字を保持
  int count = 0;//表示回数
  int playerNum;//遊ぶ人数
  int wordNum = 0;//次の人が考える文字列の変数
  int wrongPlayerNum;//間違えた人の変数
  bool wordFlag = false;//ゲームオーバー判定
  
  cout<<"ようこそ！しりとりゲームへ！\n\n";
  
  do
  {
    //プレイヤーの人数の指定
    cout<<"ゲームをする人数を選択してください。\n";
    cout<<"人数: ";
    cin>>playerNum;
    if(playerNum == 0)
    {
      cout<<"\nその人数では遊べません！\n";
    }
    
  }while(playerNum == 0);
  
  cout<<"\n"<<playerNum<<"人で遊ぶのですね！それでは、プレイヤーの名前を入力してください。\n";
  
  //プレイヤーの名前を設定
  int i;
  for(i=0; i<playerNum; i++)
  {
    cout<<i+1<<"人目の名前: ";
    cin>>name;
    nameInventory.push_back(name);
  }

  cout<<"\n全員の名前が入力されました。これより、しりとりゲームを始めます。\n";
  //ゲームはshiritoriの文字からスタートする
  cout<<"最初の単語は'"<<wordInventory[0]<<"'です。\n";
  
  do
  {
    for(int i=0; i<playerNum; i++)
    {
      //入力された文字の一文字目が前回の文字の末尾と違うとき、繰り返し入力を求める処理
      do
      {
        count++;
        if(count == 1)
        {
          lastWard = wordInventory[wordNum];//前回の文字を保管しておく
          //プレイヤーが文字を入力
          cout<<nameInventory[i]<<"さんは'"<<wordInventory[wordNum]<<"'に続く"<<lastWard.substr(lastWard.length()-1)<<"から始まる文字をローマ字か英単語で入力してください。\n";
          cin>>word;
          
          lastWard = wordInventory[wordNum];
        }
        else
        {
          cout<<"一文字目の文字が前回の単語の末尾と違います。\n";
          
          cout<<nameInventory[i]<<"さんは'"<<wordInventory[wordNum]<<"'に続く"<<lastWard.substr(lastWard.length()-1)<<"から始まる文字をローマ字か英単語で入力してください。\n";
          cin>>word;
        
          lastWard = wordInventory[wordNum];
        }
      }while(word.substr(0,1) != lastWard.substr(lastWard.length()-1));
      
      //入力された文字の末尾が'ん'のとき、このwhile文から抜け出す処理
      if(word.find('n',word.length()-1) != string::npos)
      {
        wordFlag = true;
        wrongPlayerNum = i;//間違えた人の番号を変数として取っておく
        break;
      }
      else
      {
        //一番目の人に戻る
        if(i == playerNum-1)
        {
          i = -1;
        }
        //入力された文字をwardInventoryに格納する
        wordInventory.push_back(word);
        wordNum++;
        count = 0;
      } 
    }
   
  }while(wordFlag == false);

  //ゲームオーバーの表示
  cout<<"残念～！'n'がついたので"<<nameInventory[wrongPlayerNum]<<"さんの負けです！";
  return 0;
}


＜ゲームループの図の画像＞

![スクリーンショット_20221102_135022](https://user-images.githubusercontent.com/104427265/199402673-09e4f443-c50c-4313-b08b-e043ede3ffcc.png)
