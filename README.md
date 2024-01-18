# ch11_java
package ch11_java;

import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.net.URL;
import java.util.Iterator;

import javax.net.ssl.HttpsURLConnection;

import org.json.simple.JSONArray;
import org.json.simple.JSONObject;
import org.json.simple.parser.JSONParser;
import org.json.simple.parser.ParseException;

public class ApiJson {
	
	public static void main(String[] args) throws IOException, ParseException {
		
		
		String allUrl = "https://api.upbit.com/v1/market/all";
		// URL클래스 사용 요청
		URL url = new URL(allUrl);
		HttpsURLConnection conn = (HttpsURLConnection) url.openConnection() ;
		// 요청방식 설정(get or post)
		conn.setReadTimeout(5000); //5초
		conn.setDoInput(true);
		int resCode = conn.getResponseCode(); // 응답에 따른 요청코드 리턴 200정상
		// 정상응답일때 처리
		if(resCode == HttpsURLConnection.HTTP_OK) {
			System.out.println(resCode);
			BufferedReader in = 
						new BufferedReader(new InputStreamReader(conn.getInputStream()));
			String inputLine;
			StringBuffer response = new StringBuffer();
			// 내용일 없을때 까지 버퍼에 담기
			while ((inputLine = in.readLine()) != null){
				response.append(inputLine);
				
			}
			in.close();
			System.out.println(response.toString());
			JSONParser parser = new JSONParser();
			// 응답데이터의 구조가 처음 배열
			//Json데이터 형태로 문자열을 파싱(json데이터 규칙으로 읽어드림)
			JSONArray jsonArray = (JSONArray) parser.parse(response.toString());
			for(Object object: jsonArray) {
				//응답데이터의 구조가 배열안에 객체 (key:value)형태로 담겨있음
				JSONObject jsonObj = (JSONObject) object;
				System.out.println("market:" + jsonObj.get("market"));
				System.out.println("kor:" + jsonObj.get("korean_name"));
				System.out.println("en:" + jsonObj.get("english_name"));
			}
		}
	}
	public static JSONObject getCoin(String code) {
		JSONObject obj = null;
		String detailUrl = "https://api.upbit.com/v1/ticker?markets="+code;
		URL url = new URL(obj);
		HttpsURLConnection conn = (HttpsURLConnection) url.openConnection() ;
		// 요청방식 설정(get or post)
		conn.setReadTimeout(5000); //5초
		conn.setDoInput(true);
		int resCode = conn.getResponseCode(); // 응답에 따른 요청코드 리턴 200정상
		// 정상응답일때 처리
		if(resCode == HttpsURLConnection.HTTP_OK) {
			System.out.println(resCode);
			BufferedReader in = 
						new BufferedReader(new InputStreamReader(conn.getInputStream()));
			String inputLine;
			StringBuffer response = new StringBuffer();
			// 내용일 없을때 까지 버퍼에 담기
			while ((inputLine = in.readLine()) != null){
				response.append(inputLine);
				
			}
			in.close();
			System.out.println(response.toString());
			JSONParser parser = new JSONParser();
			// 응답데이터의 구조가 처음 배열
			//Json데이터 형태로 문자열을 파싱(json데이터 규칙으로 읽어드림)
			JSONArray jsonArray = (JSONArray) parser.parse(response.toString());
			for(Object object: jsonArray) {
				//응답데이터의 구조가 배열안에 객체 (key:value)형태로 담겨있음
				JSONObject jsonObj = (JSONObject) object;
				System.out.println("market:" + jsonObj.get("market"));
				System.out.println("kor:" + jsonObj.get("korean_name"));
				System.out.println("en:" + jsonObj.get("english_name"));
			}
		}
	
		return obj;
	}
	
	
	
	
	
	
}
