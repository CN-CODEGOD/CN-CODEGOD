# POWEHELL 向量类 
[System.Numerics.Vector2] 二维空间向量
[System.Numerics.Vector3] 三维空间向量



# 计算点与线段的距离
数学：
![image](https://github.com/CN-CODEGOD/CN-CODEGOD/assets/166476136/a85b8ab8-3214-4fa3-ba7e-628e37ed73f7)

## 技巧：
利用
[System.Numerics.Vector2] 二维空间向量 类中的方法计算

## powershell 代码
  ![image](https://github.com/CN-CODEGOD/CN-CODEGOD/assets/166476136/82972f58-a89c-4ae7-9f81-dd598a95d89f)

```
static [psobject]calcroute (
    [placecoordinate]$placecoordinate
,
[psobject]$roadcoordinate


)
{ 
    

##给点确定xyz

    
    $a = @{
        x=$roadcoordinate.x
      
        z=$roadcoordinate.z
    }
    $b = @{x= $roadcoordinate.x1
    
        z=$roadcoordinate.z1
    }
    $p = $placecoordinate
#给线段，向量确定XYZ
$OP = [System.Numerics.Vector2]::new($p.x,$p.z)
$v = [System.Numerics.Vector2]::new($b.x-$a.x,$b.z-$a.z)
$u= [System.Numerics.Vector2]::new($p.x-$a.x,$p.z-$a.z)

$oa =[System.Numerics.Vector2]::new($a.x,$a.z)

$pp1 = [System.Numerics.Vector2]::new(-$v[1],$v[0])
$ap= [System.Numerics.Vector2]::new($p.x-$a.x,$p.z-$a.z)
# 利用[System.Numerics.Vector2]::dot 计算r 
$r=[System.Numerics.Vector2]::dot($v,$ap)/[System.Numerics.Vector2]::dot($v,$v)
$projectedpoint="projected point"




#根据r值确定情况
    
if ($r -gt 0 -and $r -lt 1) {
    $projectedpoint= $oa+$v*$r


    
}

elseif ($r -gt 1) {
    $projectedpoint=$b
    
    

}

elseif ($r -lt 0) {
    $projectedpoint =$a
    
    
}









#return
return
@{    roadcoordinate=$roadcoordinate
    projectedpoint=$projectedpoint
    distance=[math]::sqrt([math]::pow(($projectedpoint.x-$placecoordinate.x),2)+[math]::pow(($projectedpoint.z-$placecoordinate.z),2))
    r=$r }

    
        }

        }
```

# 计算线与线的交点

![相交](https://github.com/CN-CODEGOD/CN-CODEGOD/assets/166476136/5a8d4cd6-c7c0-437d-bef9-8d788ffa8ecc)


# 数学：
![image](https://github.com/CN-CODEGOD/CN-CODEGOD/assets/166476136/ec64d366-e2a1-4bba-9741-3cde7c2f547f)


![image](https://github.com/CN-CODEGOD/CN-CODEGOD/assets/166476136/1e400ef1-e7c7-4a61-a5e3-5435ac851faa)


# POWERSHELLL ：
```
static [psobject]lineIntersect(

[psobject]$roadcoordinate1
,
[psobject]$roadcoordinate2
)
{

    $A1=$roadcoordinate1.z1 - $roadcoordinate1.z
    $B1=$roadcoordinate1.x-$roadcoordinate1.x1
    $C1=$A1*$roadcoordinate1.x+$B1*$roadcoordinate1.z
    $A2=$roadcoordinate2.z1-$roadcoordinate2.z
    $B2=$roadcoordinate2.x- $roadcoordinate2.x1
    $C2=$A2*$roadcoordinate2.x+$B2*$roadcoordinate2.z
    $denominator=$A1*$B2-$A2*$B1


    return @{

        X=($B2*$C1-$B1*$C2)/$denominator
        Y=($A1*$C2-$A2*$C1)/$denominator

    }   

    
    
}


```
