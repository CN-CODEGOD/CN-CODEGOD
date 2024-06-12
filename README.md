# Everything  you need to know about powershell Parameter

最近几天折腾pwsh parameter
把学习的网址和经验分享给大家
把关于powershell  parameter 所有变量以及方法看了一遍，终于摸透了parameter的门路

一贴搞懂所有parameter方法
首先最简单的parameter 是这样
powershell 代码讲究的是严谨以及简洁，如何在参数方面下手，使得自己的代码更加严谨，简洁

param (
$testparameter
)

)*[/md]

这种parameter是最基本的parameter 没有其他功能和限制，后续如果想要增强自己的parameter就可以增加许多功能或者方法，使得自己的parameter增加功能或者帮助自己的脚本功能

方法一：
param[parameter( )]
这种是powershell的方法功能放的地方，里面可以放各自或者方法来限制parameter或者增强自己的脚本功能

param[paramter(mandatory)]限制parameter必须被定义

param[parameter[paramtersetname]]定义parameter的组，定义一个paramter组后，parameter必须是这个组的或者是没有组的

相关链接:

方法二：
[vaildataset()]
顾名思义vaildataset 就是有效的值，这里定义了powershell各种有效的input
[vaildateset(‘data’,data)]
[validateset([dataset])]
里面可以
相关链接:
1.https://learn.microsoft.com/en-u ... view=powershell-7.4
2.https://stackoverflow.com/questi ... l/67358119#67358119
方法三:
[cmdletbinding]
[cmdletbinding]是定义在powersheell 允许运行脚本的时候输入parameter，并且[cmdletbinding]能且只能置顶，因为它定义了下面的所有代码的parameter，你可以把它当作parameter的头子
[cmdletbinding(DefaultparametersetName)]里面还有这些方法，可以定义脚本parameter初始的一些数据
相关链接：https://learn.microsoft.com/en-u ... view=powershell-7.4

具体教学
很多人在写代码的时候不知道如何具体传输parameter
举个例子:



[CmdletBinding()]
param (
    [Parameter()]
    [string]
    $test
)


function test1 {
    param (
       $needparameter
    )
   
}
这种情况下我们只能使用[cmdletbingding]的parmeter的时候
我们从上面给这个function传输parameter呢？

简单的方法：用第一个parameter然后在代码里面写function的表达式
[CmdletBinding()]
param (
    [Parameter()]
    [string]
    $test
)


function test1 {
    param (
       $needparameter
    )
   
}

& test1 -needparamter $test



parameter具体简化以及实用：








# using mandatory



using following code powershell will ask the x y z after you call the add function, in this case you dont need to pass a lot of parameter
and getting annoying

code :

[CmdletBinding()]
param (
    [Parameter()]
    [string]
    $type
    ,
    # Parameter help description
    [Parameter()]
    [string]
    $value
)
function add {
[CmdletBinding()]
param (
    [Parameter(mandatory)]
    [int]
    $x,
    # Parameter help description
    [Parameter(mandatory)]
    [int]
    $y,
    # Parameter help description
    [Parameter(mandatory)]
    [int]
    $z
   
)
   
}
switch ($type) {
    calc {calc -type $value }
    find { find -type $value}
    remove {remove -id $value  }
    add { add -type $value -force $force }
    Default {}
   
}


# pass two layer of function :

[CmdletBinding()]
param (
    [Parameter()]
    [string]
    $action
    ,
    #
    [Parameter()]
    [string]
    $value
)


function test {
[CmdletBinding()]
param (
    [Parameter()]
    [string]
    $action
    ,
    # Parameter help description
    [Parameter(AttributeValues)]
    [string]
    $value
)
   
}


function test1 {
    [CmdletBinding()]
    param (
        [Parameter()]
        [string]
        $value
   
    )
        
    }

   
function test3 {
    [CmdletBinding()]
    param (
        [Parameter()]
        [string]
        $value
   
    )
        
    }
    switch ($action) {
        test { test -value $value }
        test1 { test1 -value $value}
        test2{ test2 -value $value }
        test3 { test3 -value $value}
    }



#simplified parameters


if we using to pass the parameter user have to remeber a lots of param when calling

but luckily we have another way to solve this problem making it eaiser

[md]```
[CmdletBinding()]
param (
    [Parameter(mandatory)]
    [string]
    $type
    ,
    #
    [Parameter()]
    [string]
    $value
   
   

)

function find {
   [CmdletBinding()]
   param (
       [Parameter(mandatory)]
       [string]
       $type
       ,
       # Parameter help description
       [Parameter(mandatory)]
       [string]
       $dimention
       ,
       # Parameter help description
       [Parameter(mandatory)]
       [string]
       $map
       ,# Parameter help description
       [Parameter(mandatory)]
       [int]
       $x
       ,
       # Parameter help description
       [Parameter(mandatory)]
       [int]
       $y
       ,
       # Parameter help description
       [Parameter(mandatory)]
       [int]
       $z

   )
   
}

function add {
    [CmdletBinding()]
    param (
        [Parameter(mandatory)]
        [string]
        $type
        ,
        # Parameter help description
        [Parameter(mandatory)]
        [string]
        $dimention
        ,
        # Parameter help description
        [Parameter(mandatory)]
        [string]
        $map
        ,# Parameter help description
        [Parameter(mandatory)]
        [int]
        $x
        ,
        # Parameter help description
        [Parameter(mandatory)]
        [int]
        $y
        ,
        # Parameter help description
        [Parameter(mandatory)]
        [int]
        $z

    )
   
}

function calc {
    [CmdletBinding()]
    param (
        [Parameter(mandatory)]
        [string]
        $type
        ,
        # Parameter help description
        [Parameter(mandatory)]
        [string]
        $dimention
        ,
        # Parameter help description
        [Parameter(mandatory)]
        [string]
        $map
        ,# Parameter help description
        [Parameter(mandatory)]
        [int]
        $x
        ,
        # Parameter help description
        [Parameter(mandatory)]
        [int]
        $y
        ,
        # Parameter help description
        [Parameter(mandatory)]
        [int]
        $z

    )
   
}
function remove {
    [CmdletBinding()]
   param (
       [Parameter(mandatory)]
       [string]
       $type
       ,
       # Parameter help description
       [Parameter(mandatory)]
       [string]
       $dimention
       ,
       # Parameter help description
       [Parameter(mandatory)]
       [string]
       $map
       ,# Parameter help description
       [Parameter(mandatory)]
       [int]
       $x
       ,
       # Parameter help description
       [Parameter(mandatory)]
       [int]
       $y
       ,
       # Parameter help description
       [Parameter(mandatory)]
       [int]
       $z

   )
   
}
switch ($type) {
    find { find -type $type }
    remove {remove -type $type}
    add {add -type $value}
    calc {calc -type $value}
}


















2.using powershell module




我们在有大量的参数需要输入的时候
应该把脚本改成powershell module 这样我们既可以在powershell里面直接输入各种方法 还可以简化代码


[md]```


function find-place {
   [CmdletBinding()]
   param (
       [Parameter(mandatory)]
       [string]
       $type
       ,
       # Parameter help description
       [Parameter(mandatory)]
       [string]
       $dimention
       ,
       # Parameter help description
       [Parameter(mandatory)]
       [string]
       $map
       ,# Parameter help description
       [Parameter(mandatory)]
       [int]
       $x
       ,
       # Parameter help description
       [Parameter(mandatory)]
       [int]
       $y
       ,
       # Parameter help description
       [Parameter(mandatory)]
       [int]
       $z

   )
   
}

function add-place{
    [CmdletBinding()]
    param (
        [Parameter(mandatory)]
        [string]
        $type
        ,
        # Parameter help description
        [Parameter(mandatory)]
        [string]
        $dimention
        ,
        # Parameter help description
        [Parameter(mandatory)]
        [string]
        $map
        ,# Parameter help description
        [Parameter(mandatory)]
        [int]
        $x
        ,
        # Parameter help description
        [Parameter(mandatory)]
        [int]
        $y
        ,
        # Parameter help description
        [Parameter(mandatory)]
        [int]
        $z

    )
   
}

function calc-place {
    [CmdletBinding()]
    param (
        [Parameter(mandatory)]
        [string]
        $type
        ,
        # Parameter help description
        [Parameter(mandatory)]
        [string]
        $dimention
        ,
        # Parameter help description
        [Parameter(mandatory)]
        [string]
        $map
        ,# Parameter help description
        [Parameter(mandatory)]
        [int]
        $x
        ,
        # Parameter help description
        [Parameter(mandatory)]
        [int]
        $y
        ,
        # Parameter help description
        [Parameter(mandatory)]
        [int]
        $z

    )
   
}
function remove-place {
    [CmdletBinding()]
   param (
       [Parameter(mandatory)]
       [string]
       $type
       ,
       # Parameter help description
       [Parameter(mandatory)]
       [string]
       $dimention
       ,
       # Parameter help description
       [Parameter(mandatory)]
       [string]
       $map
       ,# Parameter help description
       [Parameter(mandatory)]
       [int]
       $x
       ,
       # Parameter help description
       [Parameter(mandatory)]
       [int]
       $y
       ,
       # Parameter help description
       [Parameter(mandatory)]
       [int]
       $z

   )
   
}

```[/md]


4.use [validataset]
使用validataset可以有效减少大量输入时间，或者可以限制无效输入避免出现BUG

相关链接:
1.https://learn.microsoft.com/en-u ... view=powershell-7.4
2.https://learn.microsoft.com/en-u ... set%20of%20possible,matches%20an%20element%20in%20the%20supplied%20element%20set.
3.https://stackoverflow.com/questi ... l/67358119#67358119

使用
function find-place {
   [CmdletBinding()]
   param (
    []
       [Parameter(mandatory)]
       [validateset(地狱门,末影门)]
       [string]
       $type
       ,
       # Parameter help description
       [Parameter()]
       [validateset(下界,地狱,上界)]
       [string]                                                                        
       $dimention
       ,
       # Parameter help description
       [Parameter(mandatory)]
       [string]
       $map
       ,# Parameter help description
       [Parameter(mandatory)]
       [int]
       $x
       ,
       # Parameter help description
       [Parameter(mandatory)]
       [int]
       $y
       ,
       # Parameter help description
       [Parameter(mandatory)]
       [int]
       $z

   )
   
}
5.using parameter completer
自动补全大家都爱，powershell的自动输入可以运用到自己的脚本或模组里
相关链接：

使用
[md]```

function MyArgumentCompleter{
    param ( $commandName,
            $parameterName,
            $wordToComplete,
            $commandAst,
            $fakeBoundParameters )
            $possibleValues = @{
                type = @(地狱门,末影门)
                dimention = @(下界,上界,末地)

            }
if ($fakeBoundParameters.ContainsKey(Type)) {
        $possibleValues[$fakeBoundParameters.Type] | Where-Object {
            $_ -like "$wordToComplete*"
        }
    } else {
        $possibleValues.Values | ForEach-Object {$_}
    }
}


function find-place {
   [CmdletBinding()]
   param (
    []
       [Parameter(mandatory)]
       [ArgumentCompleter({ MyArgumentCompleter @args })]
       [validateset(地狱门,末影门)]
       [string]
       $type
       ,
       # Parameter help description
       [Parameter()]
       [ArgumentCompleter({ MyArgumentCompleter @args })]
       [validateset(下界,地狱,上界)]
       [string]                                                                        
       $dimention
       ,
       # Parameter help description
       [Parameter(mandatory)]
       [string]
       $map
       ,# Parameter help description
       [Parameter(mandatory)]
       [int]
       $x
       ,
       # Parameter help description
       [Parameter(mandatory)]
       [int]
       $y
       ,
       # Parameter help description
       [Parameter(mandatory)]
       [int]
       $z

   )
   
}
```[/md]





# using two layer parameters
这个方法是我自己想的把有相关性的parameter拆开然后当成一个参数输入
这样可以大大简化代码参数结构。也可以增加代码的可读性

这里我把上界，下界，末地分开来然后把他们的值变成$type 的值,然后运行的时候执行一个参数就可以同时表达俩个值了
only use when values are  related and it is not to much values to add


[md]```
function find-place {
[CmdletBinding()]
param (
    [Parameter()]
    [string]
    $下界
    ,
    # Parameter help description
    [Parameter()]
    [string]
    $上界
    ,
    # Parameter help description
    [Parameter()]
    [string]
    $末地
    ,
       # Parameter help description
       [Parameter(mandatory)]
       [string]
       $map
       ,# Parameter help description
       [Parameter(mandatory)]
       [int]
       $x
       ,
       # Parameter help description
       [Parameter(mandatory)]
       [int]
       $y
       ,
       # Parameter help description
       [Parameter(mandatory)]
       [int]
       $z
)
   
}
```[/md]





using [array] to replace xyz

这样输入不会有bug但是增加了代码的简洁性，我们写代码的时候切记要遵循这种原则，时刻要往更好的方向去写，而不是能用就行，这种代码一般很繁琐效率低下，难以更改或者改BUG


function find-place {
[CmdletBinding()]
param (
    [Parameter()]
    [string]
    $下界
    ,
    # Parameter help description
    [Parameter()]
    [string]
    $上界
    ,
    # Parameter help description
    [Parameter()]
    [string]
    $末地
    ,

# Parameter help description
[Parameter()]
[string]
$map
,
# Parameter help description
[Parameter()]
[array]
$mycoordinate
)
}


using parametersetname

这是parametersetName的一种重要用法，用来辨别输入的参数

”each parameter Name could represent each scriptblock i need to run“

function find-place {
[CmdletBinding()]
param (
    [Parameter(parametersetname=下界)]
    [string]
    $下界
    ,
    # Parameter help description
    [Parameter(parametersetname=上界)]
    [string]
    $上界
    ,
    # Parameter help description
    [Parameter(parametersetname=末地)]
    [string]
    $末地
    ,

# Parameter help description
[Parameter()]
[string]
$map
,
# Parameter help description
[Parameter()]
[array]
$mydestination

)
switch ($pscmdlet.parametersetname) {
    上界 {  }
    下界 { }
    末地{ }
}
}


其中 $pscmdlet 是重要的 parameter 参数
我们每输入参数时它的输入的参数或者输入的位置之类的参数都会记录在$pscmdlet 里面

这里是几个重要的$pscmdlet 功能
$pscmdlet.MyInvocation
$pscmdlet.MyInvocation.BoundParameters
$pscmdlet.MyInvocation.UnboundArguments
$pscmdlet.MyInvocation.Line




最后我们给参数换上class



[md]```

enum survivalplace  {
地狱门
末影门

}



Class maplist : System.Management.Automation.IValidateSetValuesGenerator {
    [string[]] GetValidValues() {
        $maplist = (get-childitem c:ex-sysxmlgps ).basename
        return [string[]] $maplist
    }
}

function find-place {
[CmdletBinding()]
param (
    [Parameter(parametersetname=下界)]
    [ArgumentCompleter({ MyArgumentCompleter @args })]
    [survival_place]
    $下界
    ,
    # Parameter help description
    [Parameter(parametersetname=上界)]
    [ArgumentCompleter({ MyArgumentCompleter @args })]

    [survival_place]
    $上界
    ,
    # Parameter help description
    [Parameter(parametersetname=末地)]
    [ArgumentCompleter({ MyArgumentCompleter @args })]

    [survival_place]
    $末地
    ,

# Parameter help description
[Parameter()]
[validateset([maplist])]
[string]
$map
,
# Parameter help description
[Parameter()]
[array]
$mydestination

)
switch ($pscmdlet.parametersetname) {
    上界 {  }
    下界 { }
    末地{ }
}
}
```[/md]

相关链接:https://learn.microsoft.com/en-u ... view=powershell-7.4

如果你需要多个parametersetname功能，你不能用上面的方法
因为一个parameter最多可以有一个parametersetname        
这是多个parameterset的参数带入方法


[md]```
   [CmdletBinding()]
   param (
       [Parameter()]
       [maplist]
       $map
       ,
       # Parameter help description
       [Parameter()]
       [survival_places]
       $overworld
       ,
       # Parameter help description
       [Parameter()]
       [survival_places]
       $nether,

       [Parameter()]
       [survival_places]
       $the_end
       ,
   
       [Parameter()]
       [string]
       $destination
   )

#根据class的名字“survival_places 确定这是你需要的组”
   $pair = foreach ($pair in $PSBoundParameters.GetEnumerator()) {
   Where-Object {$pair.values.gettype().name -like "survival_places"}
}
                    

                $destination = [place]::new($destination)
               


               
                $roads = Import-clixml c:ex-sysxmlroads.xml
                #过滤获取正确的值
                $roads|Where-Object {$_.dimention -like $pair.key}|foreach-object {
               
                    $road = [road]::new($x,$y,$z,$x1,$y1,$z1)
                    [main]::calcroad($road,$place)
               
                }|sort-object -property distance|select-object -first 1
               
         }




这些就是我所知道的关于parameter的相关知识了
&#128073;GitHub
&#128073;作者：CN_codegod
&#128073;相关书籍 https://nostarch.com/powershellsysadmins
&#128073;QQ:3468387572
&#128073;完整脚本 https://github.com/CN-CODEGOD/minecraft-GPS
