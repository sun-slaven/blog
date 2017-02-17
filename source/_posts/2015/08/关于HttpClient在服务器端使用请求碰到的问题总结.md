---
title: '关于HttpClient在服务器端使用请求碰到的问题总结'
tags:
-
categories:
- Java
date: 2015-08-12 11:21:04
---
```
static CloseableHttpClient client = null;
public static HttpEntity connectForResult(String url) {
	HttpGet get = new HttpGet(url);
    	try {
	    	client = HttpClientBuilder.create().setSSLHostnameVerifier(new NoopHostnameVerifier()).setSSLContext(new SSLContextBuilder().loadTrustMaterial(null,new TrustSelfSignedStrategy()).build()).build();
	    	CloseableHttpResponse response = client.execute(get);
		if (response.getStatusLine().getStatusCode() == HttpStatus.SC_OK) {
			HttpEntity entity = response.getEntity();
			if(entity != null) {
				System.out.println(entity);
				return entity;
			} else{
				System.out.println(&quot;entity为空！&quot;);
			}
		}
	} catch (KeyManagementException e) {
		// TODO Auto-generated catch block
		e.printStackTrace();
	catch (NoSuchAlgorithmException e) {
		// TODO Auto-generated catch block
		e.printStackTrace();
	} catch (KeyStoreException e) {
		// TODO Auto-generated catch block
		e.printStackTrace();
	} catch (ClientProtocolException e) {
		// TODO Auto-generated catch block
		e.printStackTrace();
	} catch (IOException e) {
		// TODO Auto-generated catch block
		e.printStackTrace();
	} finally {
		get.abort();
		try {
			client.close();
		} catch (IOException e) {
			// TODO Auto-generated catch block
			e.printStackTrace();
		}
	}

	return null;

}
```
以上为我个人对httpClient的一个简单封装，写了一个静态方法方便调用，但是在用的过程中，出现了一些问题。记录一下：

1.	“HttpEntity entity = response.getEntity();”这句话对相同的response对象只能使用一次。

2.	在作为静态方法时，由于使用的都是同一个client对象，所以不能在finally中写对资源的关闭，否则下一次调用就会报流关闭的错。写一个静态方法专门用于关闭资源

3. 网上说的对response.getEntity() 得到的entity对象的长度有1k长度的限制 是错的，一开始也是受这个误导查了很多资料都没找出问题。
