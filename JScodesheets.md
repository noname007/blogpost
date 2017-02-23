~~~
	export function getThumbnailName(passportName):string{
		//TODO:return seperate two char 
		var chs = passportName.match(/[^ -~]/g);
		var name = _.takeRight(chs,2);
		if(name.length<=0){
			return passportName.substr(0,2);
		}else{
			return name;
		}
	}
	export function optimize(time):string{
		if(time){
			var date = new Date(time*1000);
			var yyyy = date.getFullYear();
			var MM = date.getMonth()+1;
			var dd = date.getDate();
			var hh = date.getHours();
			var mm = date.getMinutes();
			var ss = date.getSeconds();
			return yyyy+'-'+MM+'-'+dd+' '+hh+':'+mm+':'+ss;
		}else{
			return '';
		}
	}
~~~
