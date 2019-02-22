
https://angular.cn/tutorial/toh-pt4#call-it-in-ngoninit
一、整体思路
1、	ng generate component name创建一个组件
只能这一命令的时候
在src/app/app.module.ts中执行了两步操作
①	import {nameComponent} from ‘./name/name.component’;
②	declarations: [
    AppComponent,
    nameComponent//----刚添加的
 ],
注：所以如果是手动添加的组件，需要执行这两步操作
2、	编辑里面的内容component里的selelctor是这个组件的选择器
3、在需要显示的视图中插入<selector名字></selector名字>


二、零碎知识点
1、管道
|uppercase   管道控制符合管道
Ng发布了一系列的内置管道时间，字符，金额等格式化，还可以自定义管道
{{hero.name|uppercase}}
2、双向绑定
<input [(ngModel)]=”hero.name” placeholder=”name”>
ngModel属于一个可选模块FormModule,必需先添加此模块才能正常执行ngModel指令

添加方法如下：
1、	在app.module.ts中导入FormModule
import {FormModule} from ‘@angular/forms’
2、	在元数据数组中添加FormModule
imports: [ 
BrowserModule, //原有的
FormsModule //新添加的
],
添加后就能正常运行了
3、循环
<ul>
  <li *ngFor=”let hero of heroes”>
</ul>
*ngFor是一个angular的复写器指令
4、src/style.css是基础公共样式文件
  所用于所有应用
5、显示隐藏切换
<div *ngIF=”selected”>
6、class绑定切换css样式
<li [class.selectd]=”hero ===selelctedHero”></li>
给选中的li添加 .selected 样式
7、主从组件
步骤如下：
（1）、创建一个组件ng generate component detail
Cli会自动生成四个文件（css/html/component/spec）
同时在app.module文件declarations列表中自动添加DetailComponent
（2）、在需要显示的地方添加元素控件
注：添加后显示方式
①	控制显示不显示*ngIf
②	控制显示不显示，并传值，方法如下：
1）添加@Input（）属性，在details.component文件中导入Input符号
Import {Component,OnInit,Input} from ‘@angular/core’;
2）@Input() abc: Hero;    ////////添加一个带有@Input（）装饰器的abc属性
例：export class HeroDetailComponent implements OnInit {
      @Input() abc: Hero; //////////////////////////////////////
      constructor() { }
ngOnInit() { }
}
3）在元素空间上添加属性
<app-detail [abc]=’selected’></app-detail>
detail.html内容：
<div>{{abc.name}}</div>
<div>{{abc.id}}</div>
只在选中的时候显示，并且给detail子组件传值Hero
8、服务
（1）、安装ng generate service hero 
会生成src/app/hero.service.ts文件

export class HeroService {
  constructor() { }
}
（2）、在hero.service文件中引入Hero类和HEROS数据
import { Hero } from './hero';
import { HEROES } from './mock-heros';
创建一个方法：
getHeroes():Hero []{     //引用Hero 类，返回HEROES
  return HEROES;
}
（3）、在需要用到HEROES的component文件中引入
①、import {HeroService} from ‘../hero.service’
//调用HeroService就相当于调用了HEROES和Hero
②、注入 HeroService
往构造函数中添加一个私有的 heroService，其类型为 HeroService。
constructor(private heroService: HeroService) { }
③	、添加getService（）
heroes: Hero[ ];//定义heroes属性
getService (): void { 
this.heroes = this.heroService.getHeroes(); //赋值
}
④	、在 ngOnInit 中调用它
ngOnInit() { 
this. getService ();
 }










