# -
Ts牛牛算法





const { ccclass, property } = cc._decorator;

@ccclass
export default class Helloworld extends cc.Component {



    Date1: number[] = [13, 12, 11, 9, 1]//牛五
    Date2: number[] = [11, 8, 9, 1, 1]//牛八
    Date3: number[] = [6, 7, 7, 10, 10]//牛一
    Date4: number[] = [11, 9, 1, 3, 7]//没牛
    Date5: number[] = [5, 5, 6, 13, 10]//牛七





    start() {
        console.time()
        console.timeEnd()
        this.Return3_2(this.Date1)
        this.Return3_2(this.Date2)
        this.Return3_2(this.Date3)
        this.Return3_2(this.Date4)
        this.Return3_2(this.Date5)
    }
    //---------------------------------------------------------小工具函数-----------------------------------------------------------------
    /**
     * 
     * @param num 删除数组指定元素 并且返回剩下的数组
     */
    Del(num: number, TempDate: number[]): number[] {
        let index = TempDate.indexOf(num);
        if (index > -1) {
            TempDate.splice(index, 1);
            return TempDate
        }
    }
    /**
     * 检查数组元素是否越界 
     * 如果越界10直接变成10
     */
    MoreNum(Temp2: number[]) {
        let Temp: number[] = []//创建一个临时数组
        Temp2.forEach(element => {//临时数组赋值
            if (element > 10) {
                Temp.push(10)
            } else {
                Temp.push(element)
            }
        });
        return Temp
    }
    /**
     * 拷贝一个新的数组
     */
    CopyNumArry(NumDate1: number[]) {
        let Temp: number[] = []//创建一个临时数组
        NumDate1.forEach(element => {//临时数组赋值
            Temp.push(element)
        });
        return Temp
    }
    /**
 * 常规数组求和
 */
    Sum(Temp: number[]) {
        let num: number = 0
        Temp.forEach(element => {
            num += element
        });
        return num
    }
    /**
     * 常规求余数
     */
    Surplus(Temp: number) {
        return Temp % 10
    }




    YuanZu = { "五小牛": 13, "炸弹": 12, "五花牛": 11, "牛牛": 10, "牛9": 9, "牛8": 8, "牛7": 7, "牛6": 6, "牛5": 5, "牛4": 4, "牛3": 3, "牛2": 2, "牛1": 1, "没牛": 0 }



    vvvv(num) {
        switch (num) {
            case 13:
                cc.log("五小牛")
                break;
            case 12:
                cc.log("炸弹")
                break;
            case 11:
                cc.log("五花牛")
                break;
            case 10:
                cc.log("牛牛")
                break;
            case 9:
                cc.log("牛9")
                break;
            case 8:
                cc.log("牛8")
                break;
            case 7:
                cc.log("牛7")
                break;
            case 6:
                cc.log("牛6")
                break;
            case 5:
                cc.log("牛5")
                break;
            case 4:
                cc.log("牛4")
                break;
            case 3:
                cc.log("牛3")
                break;
            case 2:
                cc.log("牛2")
                break;
            case 1:
                cc.log("牛1")
                break;
            case 0:
                cc.log("没牛")
                break;
            default:
                break;
        }
    }

    //--------------------------------------------------------------------------------------------------------------------------
    /**
     * 由于C53 等于C52  那么用C52组合排列  C52 ==10
     * @param NumDate1 目标数组
     */
    Return3_2(NumDate1: number[]) {

        let Poker = 0

        let Temp2: number[] = []//C52     包含数组2
        let Temp3: number[] = []//C53     包含数组3
        for (let i = 0; i < NumDate1.length; i++) {
            for (let j = i; j < 4;) {
                j++
                //----------------------
                //推入组合排列C52的值
                Temp2.push(NumDate1[i])
                Temp2.push(NumDate1[j])

                let Temp: number[] = this.CopyNumArry(NumDate1)//拷贝一份新的数组赋值给临时数组变量

                this.Del(Temp[j], this.Del(Temp[i], Temp))//删除临时数组2个值

                //推入临时数组C53的值
                for (let k = 0; k < Temp.length; k++) {
                    Temp3.push(Temp[k])
                }

                //Dosomething
                this.Check(Temp2, Temp3)//检测

                if (this.YuanZu[this.Check(Temp2, Temp3)] > Poker) {
                    Poker = this.YuanZu[this.Check(Temp2, Temp3)]
                }
                Temp2 = []//清空C52
                Temp3 = []//清空C53
                //---------------------
            }
        }
        //  cc.log(Poker)
        this.vvvv(Poker)
    }




    /**
     * 检测
     * 注意顺序很重要
     */
    Check(Temp2: number[], Temp3: number[]) {
        if (this.CheckWUxiaoniu(Temp2, Temp3)) {//检测是否是五小牛
            return "五小牛"
        }
        if (this.CheckBoom(Temp2, Temp3)) {//检测是炸弹
            return "炸弹"
        }
        if (this.Checkwuhuaniu(Temp2, Temp3)) {//检测是否是五花牛
            return "五花牛"
        }

        return this.CheckNum(Temp2, Temp3)
    }


    /**
     * 检测是否是五花牛
     * 
     * 是就返回真 
     * 不是就返回假的
     */
    Checkwuhuaniu(Temp2: number[], Temp3: number[]) {
        if (Temp2[0] > 10 && Temp2[1] > 10
            && Temp3[0] > 10 && Temp3[1] > 10 && Temp3[3] > 10
        ) {
            return true
        }
        else {
            false
        }
    }
    /**
     * 检测是否是五小牛
     * 
     * 是就返回真 
     * 不是就返回假的
     */
    CheckWUxiaoniu(Temp2: number[], Temp3: number[]) {
        if ((Temp2[0] < 5) && (Temp2[1] < 5)
            && (Temp3[0] < 5) && (Temp3[1] < 5) && (Temp3[2] < 5)
            && ((Temp2[0] + Temp2[1] + Temp3[0] + Temp3[1] + Temp3[2]) < 10)
        ) {
            return true
        }
        else {
            false
        }
    }
    /**
     * 检测是否是炸弹
     * 
     * 是就返回真 
     * 不是就返回假的
     */
    CheckBoom(Temp2: number[], Temp3: number[]) {
        let NewTemp = Temp2.concat(Temp3);//合并两个数组变成一个新的数组
        NewTemp.sort()//排序
        if (NewTemp[0] == NewTemp[1] && NewTemp[1] == NewTemp[2] && NewTemp[2] == NewTemp[3]) {
            return true
        }
        if (NewTemp[1] == NewTemp[2] && NewTemp[2] == NewTemp[3] && NewTemp[3] == NewTemp[4]) {
            return true
        }
        return false
    }
    /**
     * 检查牌型是否是牛牛等等
     */
    CheckNum(Temp2: number[], Temp3: number[]) {

        let fff = this.MoreNum(Temp2)
        let fff1 = this.MoreNum(Temp3)

        let dddddd = ""
        let num3 = this.Surplus(this.Sum(fff1))//先求和在求余数  三位数
        if (num3 == 0) {//3有牛
            let num2 = this.Surplus(this.Sum(fff))//先求和在求余数  两位数
            if (num2 == 0) {//2有牛
                dddddd = "牛" + "牛"
            }
            else {//2没牛
                dddddd = "牛" + num2
            }
        } else {
            dddddd = "没牛"
        }
        return dddddd
    }
}
