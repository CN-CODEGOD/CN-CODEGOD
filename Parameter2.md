# 高级parameter
```
  [CmdletBinding()]
    param (
        # parameter for teleportation_place 
        [Parameter(parametersetname="teleportation_place")]
        [switch]
        $teleportation_place
        ,
        [Parameter(parametersetname="wynncraft_place")]
        [wynncraft_place]
        $wynncraft_place
        ,
        # Parameter help description
        [Parameter(parametersetname="survival_place")]
        [survival_place]
        $survival_place
        ,
        # 
        [Parameter(parametersetname="road")]
        [road]
        $road
        ,
      
        # Parameter help description
        [Parameter()]
        [placecoordinate]
        $mycoordinate
    )

```

每个parameter都是一个独立的class
这种parameter 对比传统的parameter跟容易理解，当处理大量参数时可以简化代码，简化参数输入的 
参数的输入如下
find-place -wynncraft_place ([wynncraft_place]::new("bank"))
add-place -wynncraft_place ([wynncraft_place]::new((1,2,3),"potion_merchant"))

相比传统的参数输入，高级参数有以下特点
1.每个参数都是一个独立的class
2.每个参数的代表的是一个独立的参数集 拥有 如type，name，id等。。

什么时候使用高级参数？
1.每当需要输入的参数集是独立的，用gps为例，Wynncraft_place ,Survival_place,road等是储存在不同csv表的地图，它们都是需要输入的地图参数，我们GPS里面的function同时也是需要这些参数进行计算
2.一般高级参数都代表了一个脚本的主要参数输入，如地图，这种我们想要直接输入一个地图就需要把每个地图里面的参数写入类并用高级参数传输
高级参数的缺陷
1.一个function参数只能输入一个高级参数
2.只能输入类来传输所以必须创建新类[wynncraft_place]::new()

高级参数的优点
1.使得代码简洁明了
2.
construct：
传输的高级参数可以应用不同function，
如GPS中的
find-place 
```
function find-place {
    
        <#
.SYNOPSIS
find-place 
 -wynncraft_place ()

 -survival_place ()

-road ()

-teleportation_place ()
.DESCRIPTION
GPS module function search-place 
search the structure near around you
.PARAMETER Path
.
.PARAMETER LiteralPath
.
.EXAMPLE
find-place -wynncraft_place "bank"
____________________
placetype :
    potion_merchant
    blackSmith
    scroll_merchant
    farm
    fishing
    tool_merchant
    
    mine
    identifier
    bank
    chest
    powder_master
    housing
 
    boat 
    woodland_mansion
    ocean_mountain
    pillager_outpost
    village
    portal
    fortress
    slime_chunk
    ravine
    ocean_ruins
    fossil
    Trail_Ruins
    roads
    stronghold
    Ancient_City
    Desert_Temple
    lgloo
    Biomes
    mineshaft
    shipwreck
    cave
    lava_pool
    Geode
    apple
    ore_veins
    Derset_wellwitch_hut
_________________________________
    Dimention:
    nether
    the_end
    overworld

    Author: CN_CODEGOD
    Date: June 10, 2024

 
.NOTES


    #>

   [CmdletBinding()]
   param (
       [Parameter(parametersetname="survival_place")]
       [survival_place]
       $survival_place
       ,
       # parameter for wynncraft_place
       [Parameter(parametersetname="wynncraft_place")]
       [wynncraft_place]
       $wynncraft_place
       ,
       # parameter for road 
       [Parameter(parametersetname="road")]
       [road]
       $road
       ,
       # paramter for teleportation_place
       [Parameter(parametersetname="teleportation_place")]
       [teleportation_place]
       $teleportation_place

     
   )
   
   switch ($pscmdlet.parametersetname) {
    survival_place { 
Import-clixml c:\ex-sys\xml\survival_places.xml|Where-Object { 
    $_.type -like $survival_place.type -or $_.id -eq $survival_place.id
}
     }
    wynncraft_place{ 
        Import-clixml c:\ex-sys\xml\wynncraft_places.xml|Where-Object {
            $_.type -like $wynncraft_place.type -or $_.id -eq $wynncraft_place.id
        }
    }
    road { Import-clixml c:\ex-sys\xml\roads.xml |Where-Object{
        $_.dimention -like $road.dimention -or $_.id -eq $road.id

    } }
    teleportation_place { 

        Import-clixml c:\ex-sys\xml\teleportation_places.xml|Where-Object {$_.name -eq $teleportation_place.name -or $_.id -eq $teleportation_place.id}
    }  
    
   }



}

```


```

        function add-place {
                <#
.SYNOPSIS
add-place
-wynncraft_place (placecoordinate,type)
-survival_place (placecoordinate,dimention,type)
-teleportation (placecoordinate,name)
-road (roadcoordinate,dimention,name)
.DESCRIPTION
    GPS function .add-place 
    add structure for GPS map
.PARAMETER Path
    The path to the 
.PARAMETER LiteralPath
.
.EXAMPLE
add-place -wynncraft_place "(1,2,3),bank"

.NOTES

place_type :
    potion_merchant
    blackSmith
    scroll_merchant
    farm
    fishing
    tool_merchant
    
    mine
    identifier
    bank
    chest
    powder_master
    housing
 
    boat 
    woodland_mansion
    ocean_mountain
    pillager_outpost
    village
    portal
    fortress
    slime_chunk
    ravine
    ocean_ruins
    fossil
    Trail_Ruins
    roads
    stronghold
    Ancient_City
    Desert_Temple
    lgloo
    Biomes
    mineshaft
    shipwreck
    cave
    lava_pool
    Geode
    apple
    ore_veins
    Derset_wellwitch_hut
    nether_portal

    dimention:
    nether
    the_end 
    overworld
    Author: CNCODEGOD
    Date: June 10, 2024
#>

           [CmdletBinding()]
           param (
               [Parameter(parametersetname="road")]
               [road]
               $road
               ,
               # 
               [Parameter(parametersetname="wynncraft_place")]
               [wynncraft_place]
               $wynncraft_place
               ,
              
              
                   [Parameter(parametersetname="survival_place")]
                    [survival_place]
                   $survival_place
                   ,
                   
                   [Parameter(parametersetname="teleportation_place")]
                   [teleportation_place]
                   $teleportation_place
               )
           
        
           switch ($pscmdlet.parametersetname) {
            #parameter for add-place -road
            road {

                
                  
                    $roads = Import-clixml c:\ex-sys\xml\roads.xml
                    [road]::validate($road)
                    $id =[int]($roads|Sort-Object -Property id |Select-Object -Last 1).id+1
                  $road.id=$id
                  $roads=[System.Collections.Generic.List[road]]$road+$roads
                  $roads|export-Clixml C:\ex-sys\xml\roads.xml
                  "成功添加路线 ：{0},{1},{2}----{3},{4},{5}" -f $road.roadcoordinate.x,$road.roadcoordinate.y,$road.roadcoordinate.z,$road.roadcoordinate.x1,$road.roadcoordinate.y1,$road.roadcoordinate.z1

                }
             
              #parameter for add-place -wynncraft_place
            wynncraft_place {
                switch ($wynncraft_place.type) {
                 
                chest { $distance_limit=5}
blackSmith  { $distance_limit=5}
potion_merchant  { $distance_limit=5}
tool_merchant  { $distance_limit=5}
identifier   { $distance_limit=5}

powder_master  { $distance_limit=5}


Default {$distance_limit=50}


                }
[wynncraft_place]::validate($wynncraft_place,$distance_limit)
$wynncraft_places = Import-clixml c:\ex-sys\xml\wynncraft_places.xml
$id =[int]($wynncraft_places  |Sort-Object -Property id |Select-Object -Last 1).id+1
$wynncraft_place.id =$id
$wynncraft_places=[System.Collections.Generic.List[wynncraft_place]]$wynncraft_place+$wynncraft_places
$wynncraft_places|Export-Clixml c:\ex-sys\xml\wynncraft_places.xml

"成功添加{0},坐标为:{1},{2},{3}" -f $wynncraft_place.type ,$wynncraft_place.placecoordinate.x,$wynncraft_place.placecoordinate.y,$wynncraft_place.placecoordinate.z

             }
#parameter for add-place -survival_place
            survival_place {
         

                switch ($survival_place.type) {
                    nether_portal {$distance_limit=5  }
                    Default {$distance_limit=50  }
                    
                }
                [survival_place]::validate($survival_place,$distance_limit)
                $survival_places = Import-clixml c:\ex-sys\xml\survival_places.xml

                $id =[int]($survival_places  |Sort-Object -Property id |Select-Object -Last 1).id+1
                
            $survival_place.id=$id    
            
            $survival_places=[System.Collections.Generic.List[survival_place]]$survival_place+$survival_places
            $survival_places|Export-Clixml c:\ex-sys\xml\survival_places.xml
            "成功添加生存存档{0}坐标：{1},{2},{3}" -f $survival_place.type,$survival_place.placecoordinate.x,$survival_place.placecoordinate.y,$survival_place.placecoordinate.z

            
                 }
                 #parameter for add-place -teleportation_place
            teleportation_place {$teleportation_places = Import-clixml c:\ex-sys\xml\teleportation_places.xml
                [teleportation_place]::validate($teleportation_place,50)
            $id =[int]($teleportation_places|Sort-Object -Property id |Select-Object -Last 1).id+1
            $teleportation_place.id=$id 
            
            $teleportation_places=[System.Collections.Generic.List[teleportation_place]]$teleportation_place + $teleportation_places
            $teleportation_places|Export-Clixml c:\ex-sys\xml\teleportation_places.xml
            "成功添加传送点{0} ,坐标{1},{2},{3}" -f $teleportation_place.name,$teleportation_place.placecoordinate.x,$teleportation_place.placecoordinate.y,$teleportation_place.placecoordinate.z
           }

        }

    
    
}

```
俩个参数都需要wynncraft_place 的输入但是，每个function需要的参数不一样
find-place 需要参数place_type 或 id 
add-place 需要参数place_type,placecoordinate

placetype,placecoordinate 的construct
如下的construct可以接受placetype，placecoordinate
```
## parameter class construct for add-place -wynncraft_place
wynncraft_place ([placecoordinate]$placecoordinate,[place_type]$type) {

        $this.placecoordinate=$placecoordinate  
    $this.type =$type
}
```

place_type 或 id
如下的construct
```
## parameter class construct for search-place -wynncraft_place
wynncraft_place ([string]$value){ 
	[int]$attempt=-1
	if ([int]::TryParse($value,[ref]$attempt))
	{
		$this.id=$attempt
	}
	else
	{
        
		$this.type=$value
        $this.id=$attempt
	}
}

```
    road ([dimention]$value){ 
        [int32]$attempt=-1
        if ([int32]::TryParse($value,[ref]$attempt))
        {
            $this.id=$attempt
        }
        else
        {
            $this.dimention=$value
            $this.id=$attempt
        }
    }
    ```

    需要注意的是第一个是construct通过type来query
    第二个是通过输入value的值来query

# basic class
基础的类，这些类是组成高级参数的element


每个参数集都有一个类，但是他们同属地图，所以我们基础类（basic class）创建[placecoordinate](点坐标),[roadcoordinate](线坐标)
每次我们添加新的地图（高级参数）我们可以直接利用这些基础类（basic class）来组建高级参数


```



#element class for point coordinate



class placecoordinate {
    [int]$x
    [int]$y
    [int]$z

    static [void]validate ([array]$coordinate){
        if ($coordinate.count -ne 3) {
            throw "the coordinate is valid,please input a (x,y,z),coordinate"
        }

        
    }
    placecoordinate([array]$placecoordinate){
        [placecoordinate]::validate($placecoordinate)
        $this.x=$placecoordinate[0]
        $this.y=$placecoordinate[1]
        $this.z=$placecoordinate[2]
    }
}
#element class for line coordinate
class roadcoordinate {
[int]$x
[int]$y
[int]$z
[int]$x1    
[int]$y1
[int]$z1
roadcoordinate([array]$roadcoordinate){

    $this.x=$roadcoordinate[0]
    $this.y=$roadcoordinate[1]
    $this.z=$roadcoordinate[2]
    $this.x1=$roadcoordinate[3]
    $this.y1=$roadcoordinate[4]
    $this.z1=$roadcoordinate[5]
}
}


```
需要注意的是基础参数的construct 是接受[string],[array],[int]的，不然无法在高级参数中直接使用s


