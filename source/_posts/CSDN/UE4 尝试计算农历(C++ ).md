农历是定历，它具有天文年历的特性，能很好地和各种天象对应，如它的节气严格对应太阳高度，历日较严格地对应月相，闰月的不发生频率和发生频率对应地球近日点和远日点，其它天象如日出日没， 晨昏蒙影，五星方位，日月食，潮汐等，就连历月也大致对应太阳高度。所以农历的计算更为繁琐一点，而且农历历月的天数只有29日和30日两种。
代码展示：

```cpp
.h
// Fill out your copyright notice in the Description page of Project Settings.

#pragma once

#include "CoreMinimal.h"
#include "GameFramework/Pawn.h"
#include "MyPawn.generated.h"

UCLASS()
class TEST2_API AMyPawn : public APawn
{
	GENERATED_BODY()

public:
	// Sets default values for this pawn's properties
	AMyPawn();

public:	

	// 是否存在农历的闰月,并返回闰月,没有闰月返回零
	UFUNCTION(BlueprintCallable)
	int32 GetLeapMonth(int32 LunarYear);

	// 返回闰月的天数 : 2020年闰四月29天
	UFUNCTION(BlueprintCallable)
	int32 GetLeapMonthDays(int32 LunarYear);

	// 农历当年月天数
	UFUNCTION(BlueprintCallable)
	int32 GetLunarCurentMonthDays(int32 LunarYear, int32  LunarMonth);

	// 公历转农历函数
	UFUNCTION(BlueprintCallable)
	int32 SolarToLunar(int32 year, int32 month, int32 day);

	// 获取公历的当月天数
	UFUNCTION(BlueprintCallable)
	int32 SloarMonthDays(int32 year, int32 month);

	// 从公历从1900.1.31(农历1900.1.1)到今天的总天数
	UFUNCTION(BlueprintCallable)
	int32 GetSolarTotalDays(int32 year, int32 month, int32 day);

	// 获取今年已经过去多少天了
	UFUNCTION(BlueprintCallable)
	int32 GetThisYearSoFarDays(const int32 Year, const int32 Month, const int32 Day);

	// 获取农历当年总天数
	UFUNCTION(BlueprintCallable)
	int32 GetLunarYearTotalDays(int32 Year);

	// 是否是闰年函数
	UFUNCTION(BlueprintCallable)
	bool GetLeapYear(int32 Year);

private:

	unsigned long int LunarInfo[151] =
	{
		0x04bd8,0x04ae0,0x0a570,0x054d5,0x0d260,0x0d950,0x16554,0x056a0,0x09ad0,0x055d2,//1900---1909
		0x04ae0,0x0a5b6,0x0a4d0,0x0d250,0x1d255,0x0b540,0x0d6a0,0x0ada2,0x095b0,0x14977,//1910
		0x04970,0x0a4b0,0x0b4b5,0x06a50,0x06d40,0x1ab54,0x02b60,0x09570,0x052f2,0x04970,//1920
		0x06566,0x0d4a0,0x0ea50,0x06e95,0x05ad0,0x02b60,0x186e3,0x092e0,0x1c8d7,0x0c950,//1930
		0x0d4a0,0x1d8a6,0x0b550,0x056a0,0x1a5b4,0x025d0,0x092d0,0x0d2b2,0x0a950,0x0b557,//1940
		0x06ca0,0x0b550,0x15355,0x04da0,0x0a5b0,0x14573,0x052b0,0x0a9a8,0x0e950,0x06aa0,//1950
		0x0aea6,0x0ab50,0x04b60,0x0aae4,0x0a570,0x05260,0x0f263,0x0d950,0x05b57,0x056a0,//1960
		0x096d0,0x04dd5,0x04ad0,0x0a4d0,0x0d4d4,0x0d250,0x0d558,0x0b540,0x0b6a0,0x195a6,//1970
		0x095b0,0x049b0,0x0a974,0x0a4b0,0x0b27a,0x06a50,0x06d40,0x0af46,0x0ab60,0x09570,//1980
		0x04af5,0x04970,0x064b0,0x074a3,0x0ea50,0x06b58,0x055c0,0x0ab60,0x096d5,0x092e0,//1990
		0x0c960,0x0d954,0x0d4a0,0x0da50,0x07552,0x056a0,0x0abb7,0x025d0,0x092d0,0x0cab5,//2004
		0x0a950,0x0b4a0,0x0baa4,0x0ad50,0x055d9,0x04ba0,0x0a5b0,0x15176,0x052b0,0x0a930,//2010
		0x07954,0x06aa0,0x0ad50,0x05b52,0x04b60,0x0a6e6,0x0a4e0,0x0d260,0x0ea65,0x0d530,//2028
		0x05aa0,0x076a3,0x096d0,0x04bd7,0x04ad0,0x0a4d0,0x1d0b6,0x0d250,0x0d520,0x0dd45,//2030
		0x0b5a0,0x056d0,0x055b2,0x049b0,0x0a577,0x0a4b0,0x0aa50,0x1b255,0x06d20,0x0ada0,//2040--2049
		0x055b0,
	};

	int32 m_uilunaryear;
	int32 m_uilunarmonth;
	int32 m_uilunarday;
};
```

```cpp
// Fill out your copyright notice in the Description page of Project Settings.

#include "MyPawn.h"


// Sets default values
AMyPawn::AMyPawn()
{
 	// Set this pawn to call Tick() every frame.  You can turn this off to improve performance if you don't need it.
	PrimaryActorTick.bCanEverTick = true;

	 m_uilunaryear = 0;
	 m_uilunarmonth = 0;
	 m_uilunarday = 0;

}

int32 AMyPawn::GetLeapMonth(int32 LunarYear)
{
	// 0x 是十六进制的前导符， f 表示 16进制的值 15 ，0xf 就是表示十六进制的f
	return LunarInfo[LunarYear - 1900] & 0xf;
}

int32 AMyPawn::GetLeapMonthDays(int32 LunarYear)
{
	if (GetLeapMonth(LunarYear))
		// 0x10000:0x是十六进制的前导符,所以这是一个十六进制数，数值为10000。转换成十进制数 ：1 x 164 + 0 x 163+ 0 x 162 + 0 x 161 + 0 x 16 0 = 65536
		return(((LunarInfo[LunarYear - 1900]) & 0x10000) ? 30 : 29);
	else
		return (0);
}

int32 AMyPawn::GetLunarCurentMonthDays(int32 LunarYear, int32 LunarMonth)
{
	// ">>" 1. 用到输出语句cout时会用到这个，表示输出。2. 与变量在一起的时候表示左移操作，相当于乘以2。
	return((LunarInfo[LunarYear - 1900] & (0x10000 >> LunarMonth)) ? 30 : 29);
}

int32 AMyPawn::SolarToLunar(int32 year, int32 month, int32 day)
{
	int32 totalday = 0; // 记录农历1900.1.1日到今天相隔的天数
	int32 runyueflag = 0; //标记是否有闰月
	int32 LeapMonth = 0;
	int32 yearflag = 0;

	// 判断农历的时间在 1900 - 2049 年区间
	if (year < 1901 || year > 2049 || month > 12 || month == 0 || (year == 1900 && month == 1)) return 0;

	// SloarMonthDays 获取这个月的天数（公历）
	if (day > SloarMonthDays(year, month) || day == 0)
		return 0;
	//计算1900.1.1 到  输入年月的天数
	totalday = GetSolarTotalDays(year, month, day);
	m_uilunaryear = 1900;

	while (totalday > 385) // 385 大于一年 剩余一年用于条件计算
	{
		totalday -= GetLunarYearTotalDays(m_uilunaryear); 
		m_uilunaryear++;
	}
	if (totalday > GetLunarYearTotalDays(m_uilunaryear))  // 排除m_uilunaryear有闰月的情况
	{
		totalday -= GetLunarYearTotalDays(m_uilunaryear);
		m_uilunaryear++;
	}
	LeapMonth = GetLeapMonth(m_uilunaryear);  // 当前闰哪个月
	if (LeapMonth)
		runyueflag = 1; // 有闰月则一年为13个月
	else
		runyueflag = 0;  // 没闰月则一年为12个月

	if (totalday == 0)   // 刚好一年
	{
		m_uilunarday = GetLunarCurentMonthDays(m_uilunaryear, 12);
		m_uilunarmonth = 12;
	}
	else
	{
		m_uilunarmonth = 1;
		while (m_uilunarmonth <= 12)
		{
			if (totalday > GetLunarCurentMonthDays(m_uilunaryear, m_uilunarmonth))
			{
				totalday = totalday - GetLunarCurentMonthDays(m_uilunaryear, m_uilunarmonth);  // 该年该月天数
				if (runyueflag == 1 && m_uilunarmonth == LeapMonth )  // 闰月处理
				{
					if (totalday > GetLeapMonthDays(m_uilunaryear))
					{
						totalday -= GetLeapMonthDays(m_uilunaryear);  // 该年闰月天数
					}
					else
					{
						m_uilunarday = totalday;
						break;
					}
					runyueflag = 0;
				}
				m_uilunarmonth++;
			}
			else
			{
				m_uilunarday = totalday;
				break;
			}
		}
	}
	FString RiQi = FString::FromInt(m_uilunaryear) + "-" + FString::FromInt(m_uilunarmonth) + "-" + FString::FromInt(m_uilunarday);
	GEngine->AddOnScreenDebugMessage(-1, 1000.f, FColor::Red, RiQi);
	return m_uilunarday;
}

int32 AMyPawn::SloarMonthDays(int32 year, int32 month)
{
	if (month == 1 || month == 3 || month == 5 || month == 7 || month == 8 || month == 10 || month == 12)
	{
		return 31;
	}
	if (month == 4 || month == 6 || month == 9 || month == 11)
	{
		return 30;
	}
	if (month == 2)
	{
		if ((year % 4 == 0 && year % 100 != 0) || year % 400 == 0)
		{
			return 29;
		}
		return 28;
	}
	return 0;
}

int32 AMyPawn::GetSolarTotalDays(int32 year, int32 month, int32 day)
{
	int32 NumberOfDays = 0;
	int32 YearBegin = 1900;
	int32 MonthBegin = 1;
	int32 DayBegin = 31;

	if (YearBegin == year)
	{
		return GetThisYearSoFarDays(year, month, day) - GetThisYearSoFarDays(YearBegin, MonthBegin, DayBegin - 1);
	}

	if (YearBegin < year)
	{
		for (int32 i = YearBegin; i < year; i++)
		{
			NumberOfDays = NumberOfDays + 365 + (i % 4 == 0 && i % 100 != 0 || i % 400 == 0);
		}

		NumberOfDays = NumberOfDays - GetThisYearSoFarDays(YearBegin, MonthBegin, DayBegin - 1) + GetThisYearSoFarDays(year, month, day);
	}

	return NumberOfDays;
}

int32 AMyPawn::GetThisYearSoFarDays(const int32 Year, const int32 Month, const int32 Day)
{
	int32 InDay = Day;

	for (int32 i = 1; i < Month; i++)
	{
		InDay +=  SloarMonthDays(Year, i);
	}

	return InDay;
}

int32 AMyPawn::GetLunarYearTotalDays(int32 Year)
{
	int Day = 0;
	for (int32 i = 1; i < 13; i++)
	{
		Day += GetLunarCurentMonthDays(Year, i);
	}
	if (GetLeapMonth(Year))
	{
		Day += GetLeapMonthDays(Year);
	}

	return Day;
}

bool AMyPawn::GetLeapYear(int32 Year)
{
	if ((Year % 4 == 0 && Year % 100 != 0) || Year % 400 == 0)
	{
		return true;
	}
	return false;
}
```
这里用的是UE4 C++编写，仅供参考！！！！

思路：

 1. 通过 LunarInfo 数组的值 “0x04bd8”（注1）可获得 
 	（1）农历的每月天数
 	（2）当年是否有闰月
 	（3）闰月当月的天数
 2. 公历转换农历，公历 1900.1.31 === 农历 1900.1.1
 	 通过当前日期获取距离1900.1.31已经过去多少天，用算出过去天数减去过去几年的天数，留下最后一年的天数进行计算。
 3. 用最后一年的天数，从第一月开始计算，最后得出今年的天数
 
 注：
	1980年的数据是： 0x095b0
	二进制：0000 1001 0101 1011 0000
	1-4: 表示当年有无闰年知，有的话，为闰月的月份，没有的话，为0。
	5-16：为除了闰月外的正常月份是大月还道是小月，1为30天，0为29天。
	注意：从1月到12月对应版的是第16位到第5位。
	17-20：表示闰月是大月还是小月，仅当存在闰月的情况下有意义。

参考：
[https://zhidao.baidu.com/question/133523583.html](https://zhidao.baidu.com/question/133523583.html)
