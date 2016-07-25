<!DOCTYPE html>
<html>
<head>
	<meta charset="utf-8">
	<title></title>
	<style type="text/css">
		img{
			position: absolute;
			margin: 0;
			padding: 0;
			left: 0;
			top: 0;
		}
	</style>
	<script type="text/javascript">
		window.onload = function(){
			var arr = [];
			document.onmousedown = function(e){
				e = e || event;
				myPreventDafault(e);
				if(e.button == 0 || e.button == 1){
					document.onmousemove = function(e){
					e = e || event;
					var x = e.clientX;
					var y = e.clientY;
					//console.log(y);
					var div = document.createElement("div");
					
					div.style.cssText = "width:3px;height:3px;background:red;left:" + x + "px;top:" + y + "px;position:absolute;";
					document.body.appendChild(div);
					//console.log(div);	
					var xy = [x,y,div];
					arr.push(xy);

					}

				}
				
				document.onmouseup = function(){
					document.onmousemove = null;
					
					//console.log(arr);

					var timer = setInterval(function(){
						var img = document.getElementById("img1");
						img.src = "img/2.gif"
						

						if(arr.length == 0){
							clearInterval(timer);
							img.src = "img/1.gif";
						}
						else{
							img.style.cssText = "left:" + arr[0][0] + "px;top:" + arr[0][1] + "px;";
							document.body.removeChild(arr[0][2]);
							arr.shift();
						}

					},30);
					
				}

			}

		}

		function myPreventDafault(eObj){
			if(eObj.preventDafault){//支持执行if
				eObj.preventDafault();
			}
			else{
				eObj.returnValue = false;
			}
		}
	</script>
</head>
<body>
	<img id="img1" src="img/1.gif" />
</body>
</html>
