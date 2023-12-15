var com = new Object();
com.kakao = new Object();
com.kakao.talk = new Object();

var com = {};
com.kakao = {};
com.kakao.talk = {};

com.kakao.talk.KakaoLink = function(appid, appver, url, msg, appname, metainfo) {
	this.msg = encodeURIComponent(msg);
	this.url = encodeURIComponent(url);
	this.appId = encodeURIComponent(appid);
	this.version = encodeURIComponent(appver);
	this.appname = encodeURIComponent(appname);
	if (typeof metainfo == "undefined") {
		this.type = "link";
	} else {
		this.type = "app";
	}

	this.apiver = "2.0";

	$(document).find("body").append(
				"<iframe id='____kakaolink____'></iframe>");
	$("#____kakaolink____").hide();
	

	try {
		if (isEmptyString(this.appId) || isEmptyString(this.version)
				|| isEmptyString(this.url) || isEmptyString(this.appname)) {
			throw "IllegalArgumentException";
		}
	} catch (e) {
		if (e == "IllegalArgumentException") {
			// error
		}
	}

	var sb = new com.kakao.talk.StringBuilder("kakaolink://sendurl?");
	sb.append("appid=").append(this.appId).append("&appver=").append(
			this.version).append("&url=").append(this.url).append("&type=")
			.append(this.type).append("&apiver=").append(this.apiver).append(
					"&appname=").append(this.appname);
	if (!this.isEmptyString(this.msg)) {
		sb.append("&msg=").append(this.msg);
	}

	if (typeof metainfo != "undefined") {
		sb.append("&metainfo=").append(JSON.KakaoStringify(metainfo));
	}
	this.data = sb.toString();
};

com.kakao.talk.StringBuilder = function(value) {
	this.strings = new Array("");
	this.append(value);
};
com.kakao.talk.StringBuilder.prototype.append = function(value) {
	if (value) {
		this.strings.push(value);
	}
	return this;
};
com.kakao.talk.StringBuilder.prototype.toString = function() {
	return this.strings.join("");
};

com.kakao.talk.KakaoLink.prototype.isEmptyString = function(str) {
	if (str.replace(/^\s*/, "").replace(/\s*$/, "").length == 0)
		return true;
	return false;
};

com.kakao.talk.KakaoLink.prototype.getData = function() {
	return this.data;
};

com.kakao.talk.KakaoLink.prototype.execute = function(callback) {
	var clickedAt = +new Date;
	setTimeout(
			function() {
				if (+new Date - clickedAt < 2000) {
					var uagent = navigator.userAgent.toLocaleLowerCase();
					// android, iphone not installed kakaotalk
					if (typeof callback == 'function') {
						callback.call(this);
					} else if (uagent.search("android") > -1) {
						$("#____kakaolink____").attr("src",
								"market://details?id=com.kakao.talk");
					} else if (uagent.search("iphone") > -1) {
						$("#____kakaolink____")
								.attr("src",
										"items://itunes.apple.com/us/app/kakaotalk/id362057947?mt=8");
					}
				}
			}, 500);
	$("#____kakaolink____").attr("src", this.data);
};

function MetaInfo(metainfo) {
	this.metainfo = metainfo;
}

JSON.KakaoStringify = JSON.KakaoStringify || function(obj) {
	var t = typeof (obj);
	if (t != "object" || obj === null) {
		// simple data type
		if (t == "string")
			obj = '"' + obj + '"';
		return String(obj);
	} else {
		// recurse array or object
		var n, v, json = [], arr = (obj && obj.constructor == Array);
		for (n in obj) {
			v = obj[n];
			t = typeof (v);
			if (t == "string")
				v = '"' + v + '"';
			else if (t == "object" && v !== null)
				v = JSON.KakaoStringify(v);
			json.push((arr ? "" : '"' + n + '":') + String(v));
		}
		return (arr ? "[" : "{") + String(json) + (arr ? "]" : "}");
	}
};