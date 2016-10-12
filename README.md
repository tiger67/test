# picture

 a angular.module('project')
 .directive('imgShow',[function(){
            return {
                retrict:'A',
                link:function(scope,element,attrs){
                    var $el=angular.element(element);
                    var a=attrs.imgShow.split(",");
                    var w=a[0];
                    var h=a[1];
                    var sp=a[2];
                    var notcenter=a[3];
                    if(notcenter && notcenter=='notcenter'){
                        $el.parent().css({display:"inline-block",width:w+"px",height:h+"px",overflow:'hidden',outline:'none'});/*verticalAlign:'middle',*/
                    }else{
                        $el.parent().css({textAlign:'center',display:"inline-block",width:w+"px",height:h+"px",overflow:'hidden',outline:'none'});/*verticalAlign:'middle',*/

                    }
                    element[0].onload=function(){
                        var nw=element[0].naturalWidth;
                        var nh=element[0].naturalHeight;
                        if(sp&&sp=='sp'){
                            if(nh<h){
                                h=nh;
                            }
                            $el.parent().css({height:h+"px"});
                        }

                        if(nw<=w&&nh<=h){
                            $el.css("width",nw+'px');
                            $el.css("height",nh+"px");
                        }else if(nw<=w&&nh>=h){
                            $el.css("width",nw+'px');
                            $el.css("height",nh+"px");
                            var m=(h-nh)/2;
                            $el.css("margin-top",m+'px').css("margin-bottom",m+'px');
                        }else if(nw>=w&&nh<=h){

                            if(sp&&sp=='sp'){
                                $el.css("width",w+'px');
                                $el.css("height",'auto');
                                $el.parent().css('height','auto');
                            }else{
                                $el.css("width",nw+'px');
                                $el.css("height",nh+"px");
                                var m=(w-nw)/2;
                                $el.css("margin-left",m+'px').css("margin-right",m+'px');
                            }

                        }else{
                            if(nw/nh==w/h){
                            }else if (nw/nh>w/h){

                                if(sp&&sp=='sp'){
                                    $el.css("width",w+'px');
                                    $el.css("height",'auto');
                                    $el.parent().css('height','auto');
                                }else{
                                    var sw=nw*h/nh;
                                    var m=(w-sw)/2;
                                    $el.css("width",sw+'px');
                                    $el.css("margin-left",m+'px').css("margin-right",m+'px');
                                }

                            }else{
                                var sh=nh*w/nw;
                                var m=(h-sh)/2;
                                $el.css("height",sh+'px')
                                $el.css("margin-top",m+'px').css("margin-bottom",m+'px');

                            }
                        }

                    }
                }
            }
        }])

