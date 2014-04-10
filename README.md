
# Mathmafic
## 概要
三年計画で数学ハンドブックをまとめグラフを添えてWebに公開する。

## 環境
 + マークダウン
 	 + HTML Build
 + 数式
 	 + Latex
 + グラフ
 	 + JavaScript


# 数式の挿入について
色々調べているとTeXに行き着いた

# 数式を簡単に使う方法

## Google Chart Tools API
[Webで数式を簡単に使う方法](https://oku.edu.mie-u.ac.jp/~okumura/blog/node/2533)  
Google Chart Tools APIを使うやり方。

<img src="http://chart.apis.google.com/chart?cht=tx&amp;chl=x=\frac{-b\pm\sqrt{b^2-4ac}}{2a}" alt="" />
	
おしい！
ちょっと文字がおかしい。


## Tex equation editor
[Tex equation editor](http://atomurl.net/math/)
これは便利そう。方程式をクリックすると、texコマンドが出てくる。

<img src="http://chart.apis.google.com/chart?cht=tx&chl=%5Cvec%7BF%7D%3Dm%20%5Cfrac%7Bd%20%5Cvec%7Bv%7D%7D%7Bdt%7D%20%2B%20%5Cvec%7Bv%7D%5Cfrac%7Bdm%7D%7Bdt%7D%20">

## js.Math

## MathJax
[MathJaxの使い方](http://genkuroki.web.fc2.com/)  

簡単な使い方：次を HTML ファイルの <head> と </head> のあいだに挿入する。それだけで LaTeX 方式で数式を書けるようになる。

	<script type="text/x-mathjax-config">
	  MathJax.Hub.Config({ tex2jax: { inlineMath: [['$','$'], ["\\(","\\)"]] } });
	</script>
	<script type="text/javascript"
	  src="http://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-AMS_HTML">
	</script>
	<meta http-equiv="X-UA-Compatible" CONTENT="IE=EmulateIE7" />

最も簡単な使い方：次を HTML ファイル中の <head> と </head> のあいだに挿入する。それだけで LaTeX 方式で数式を書けるようになる。ただし $ $ は使えない。

	<script type="text/javascript"
	  src="http://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-AMS_HTML">
	</script>

[MathJax　Preview](http://genkuroki.web.fc2.com/MathJax/LivePreviewMathJax-jquery.html) 


ブログなどでの設定

ブログなどで MathJax を使いたければ以下のコードをテンプレートのヘッダに貼り付ければよい。たったそれだけで設定は終わり。FC2ブログとライブドアブログとSo-netブログでは可能なことを確認してある。他にも便利 MathJax が使える無料ブログは結構あるようだ。

	<script type="text/x-mathjax-config">
	  MathJax.Hub.Config({ tex2jax: { inlineMath: [['$','$'], ["\\(","\\)"]] } });
	</script>
	<script type="text/javascript"
	  src="http://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-AMS_HTML">
	</script>
	<meta http-equiv="X-UA-Compatible" CONTENT="IE=EmulateIE7" />
	$ $ も IE8 対策も必要ないのであれば次の3行だけで十分である。

	<script type="text/javascript"
	  src="http://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-AMS_HTML">
	</script>

設定とマクロの共有

設定とマクロが書かれたファイル MyConfig.js を用意しておき、次のようにして読み込めば複数の HTML ファイルで同じ設定とマクロを共有できる。

	<script type="text/javascript"
	  src="http://domain/dir/MathJax/MyConfig.js"></script>
	<script type="text/javascript"
	  src="http://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-AMS_HTML">
	</script>

MathJax のデフォルトの設定からの差分を MyConfig.js に書いておくならば config=TeX-AMS_HTML の部分を config=default とすればよい。 (個人的に TeX-AMS_HTML の設定はかなり使い易いと思っている。)

MyConfig.js の中身は次のような感じにする。

	MathJax.Hub.Config({
	  tex2jax: {
	    inlineMath: [ ['$','$'], ["\\(","\\)"] ],
	    displayMath: [ ['$$','$$'], ["\\[","\\]"] ]
	  },
	  TeX: {
	    Macros: {
	      C: '{\\mathbb C}',
	      R: '{\\mathbb R}',
	      Q: '{\\mathbb Q}',
	      Z: '{\\mathbb Z}',
	      diag: '\\mathop{\\mathrm{diag}}\\nolimits',
	      np: ['{#1}#2{#1}', 2]
	    }
	  }
	});
	
例：MyConfig


# グラフ挿入の調査

## Google Image Chart Editor
Googleはなんでもある。

## [graph.tk](http://kenz0.s201.xrea.com/weblog/2012/02/graphtk.html)  
やっと出会えた。

### API
[API](http://graph.tk/about/api.html)  

### Old Method
<iframe src="http://graph.tk/#y=sin(x)" style="width:500px;height:400px"></iframe>

		<iframe src="http://graph.tk/#y=sin(x)"></iframe>

### Powerful Method
<iframe src="http://graph.tk/" id="my_graph" style="width:500px;height:400px"></iframe>
<script>
var my_graph=document.getElementById("my_graph");
my_graph.onload=function(){
function g(m){
my_graph.contentWindow.postMessage(m,"http://graph.tk");
};
g("add:x^3+1");
g("add:e^x");
//  g("block"); - Block movement by user
g("center:0,0");
}
//Methods include: add, block, empty, scale, translate, center
</script>


	<iframe src="http://graph.tk/" id="my_graph" style="width:500px;height:400px">
	</iframe>
	<script>
	var my_graph=document.getElementById("my_graph");

	my_graph.onload=function(){
	    function g(m){
	        my_graph.contentWindow.postMessage(m,"http://graph.tk");
	    };
	    g("add:x^3+1");
	    g("add:e^x");
	//  g("block"); - Block movement by user
	    g("center:0,0");
	}

	//Methods include: add, block, empty, scale, translate, center
	</script>