```php
<?php
	class Tree{

	 static public function SortTree($data, $pid = 0, $level=0, $icon = array('&ensp;├─', '&ensp;└─','&ensp;│'))
	    {
	       $str="";$arr=[]; 
	       if(empty($data)) return array();
	        foreach ($data as $k=>$v) {
	            if ($v['pid'] == $pid) {
	                $v['level']= $level+1;
	            	if($v['level']>2){
	                    $str=str_repeat($icon[2], $v['level']-2);
	                }
	                if($v['pid']== 0){
	                	$v['html']='';
	                }else{
			    		$v['html']= $str . $icon[0];
			    	}
			    	
		            $arr[] =$v;
	            	$arr = array_merge($arr, self::SortTree($data, $v['cid'], $level + 1));
					
	            }	
	        }
	        return $arr;
	    }
	    static public function getTree($data,$icon = array('&ensp;├─', '&ensp;└─','&ensp;│')){
	    	if(!is_array($data) || empty($data)) return array();
	    	$arr = self::SortTree($data, $pid = 0, $level=0, $icon = array('&ensp;├─', '&ensp;└─','&ensp;│'));
	    	foreach ($arr as $k => $v) {
	            $str = ""; 
	            if ($v['level'] > 2) {
	                for ($i = 1; $i < $v['level'] - 1; $i++) {
	                    $str .= "&ensp;│";
	                }
	            }
               	 if($v['level']!=1){
                	if (isset($arr[$k + 1]) && $arr[$k + 1]['level'] >= $arr[$k]['level']) {
	                    $arr[$k]['html'] =$str . $icon[0];
	                } else {
	                    $arr[$k]['html'] = $str .  $icon[1];
	                }
                }else{
                	$arr[$k]['html'] = $v['html'];
                }

	    	}
	    	return $arr;
	    }

	   


	}

	$data=array(
	    ['cid' => 1, 'pid' => 0,'name'=>'a1'],
	    ['cid' => 2, 'pid' => 1,'name'=>'a2'],
	    ['cid' => 3, 'pid' => 2,'name'=>'a3'],
	    ['cid' => 4, 'pid' => 2,'name'=>'a4'],

	    ['cid' => 5, 'pid' => 0,'name'=>'a5'],
	    ['cid' => 6, 'pid' => 5,'name'=>'a6'],
	    ['cid' => 7, 'pid' => 6,'name'=>'a7'],
	    ['cid' => 8, 'pid' => 7,'name'=>'a8'],
	    ['cid' => 9, 'pid' => 7,'name'=>'a9'],
	    ['cid' => 10, 'pid' => 8,'name'=>'a10'],
	    ['cid' => 11, 'pid' => 10,'name'=>'11'],
	    ['cid' => 12, 'pid' => 11,'name'=>'12'],
	    ['cid' => 13, 'pid' => 12,'name'=>'13'],
	    ['cid' => 14, 'pid' => 13,'name'=>'14'],
	    ['cid' => 15, 'pid' => 14,'name'=>'15'],
	    ['cid' => 16, 'pid' => 15,'name'=>'16'],
	    
	);
		$tree=new Tree();
		$a=$tree->getTree($data);
	    foreach ($a as $k=>$v){

	    	echo $v['html'].$v['name'].' ---level:'.$v['level'].'<br>';
	    	
	    }
最终结果
// a1 ---level:1
//  ├─a2 ---level:2
//  │ ├─a3 ---level:3
//  │ └─a4 ---level:3
// a5 ---level:1
//  ├─a6 ---level:2
//  │ ├─a7 ---level:3
//  │ │ ├─a8 ---level:4
//  │ │ │ ├─a10 ---level:5
//  │ │ │ │ ├─11 ---level:6
//  │ │ │ │ │ ├─12 ---level:7
//  │ │ │ │ │ │ ├─13 ---level:8
//  │ │ │ │ │ │ │ ├─14 ---level:9
//  │ │ │ │ │ │ │ │ ├─15 ---level:10
//  │ │ │ │ │ │ │ │ │ └─16 ---level:11
//  │ │ └─a9 ---level:4
```

