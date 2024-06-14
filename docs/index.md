# 视觉应用所需功能：

### 一、建立模版

#### 1. 灰度匹配

- `create_ncc_model`：创建灰度模型

```yaml
- `create_ncc_model (Image : input, Row : input, Column : input, AngleStart : input, AngleExtent : input, PyramidLevel : input, Contrast : input, MinContrast : input, ModelID : output)`
  - `Image`：用于创建模型的图像
  - `Row`：模型的中心行坐标
  - `Column`：模型的中心列坐标
  - `AngleStart`：搜索的起始角度
  - `AngleExtent`：搜索的角度范围
  - `PyramidLevel`：金字塔层数
  - `Contrast`：对比度参数
  - `MinContrast`：最低对比度
  - `ModelID`：输出的模型ID
```

- `find_ncc_model`：在图像中查找灰度模型

```yaml
- `find_ncc_model (Image : input, ModelID : input, AngleStart : input, AngleExtent : input, MinScore : input, NumMatches : input, MaxOverlap : input, SubPixel : input, NumLevels : input, Greediness : input, Row : output, Column : output, Angle : output, Score : output)`
  - `Image`：待匹配的图像
  - `ModelID`：之前创建的模型ID
  - `AngleStart`：搜索的起始角度
  - `AngleExtent`：搜索的角度范围
  - `MinScore`：最低匹配分数
  - `NumMatches`：最大匹配数量
  - `MaxOverlap`：匹配间的最大重叠度
  - `SubPixel`：亚像素精度
  - `NumLevels`：金字塔层数
  - `Greediness`：贪婪度
  - `Row`：匹配的位置行坐标
  - `Column`：匹配的位置列坐标
  - `Angle`：匹配的角度
  - `Score`：匹配的分数
```

#### 2. 模板匹配

- `create_shape_model`：创建形状模型

```yaml
- `create_shape_model (Image : input, NumLevels : input, AngleStart : input, AngleExtent : input, AngleStep : input, Optimization : input, Metric : input, Contrast : input, MinContrast : input, ModelID : output)`
  - `Image`：用于创建模型的图像
  - `NumLevels`：金字塔层数
  - `AngleStart`：搜索的起始角度
  - `AngleExtent`：搜索的角度范围
  - `AngleStep`：角度步长
  - `Optimization`：优化等级
  - `Metric`：匹配度量
  - `Contrast`：对比度参数
  - `MinContrast`：最低对比度
  - `ModelID`：输出的模型ID
```

- `find_shape_model`：在图像中查找形状模型

```yaml
- `find_shape_model (Image : input, ModelID : input, AngleStart : input, AngleExtent : input, MinScore : input, NumMatches : input, MaxOverlap : input, SubPixel : input, NumLevels : input, Greediness : input, Row : output, Column : output, Angle : output, Score : output)`
  - `Image`：待匹配的图像
  - `ModelID`：之前创建的模型ID
  - `AngleStart`：搜索的起始角度
  - `AngleExtent`：搜索的角度范围
  - `MinScore`：最低匹配分数
  - `NumMatches`：最大匹配数量
  - `MaxOverlap`：匹配间的最大重叠度
  - `SubPixel`：亚像素精度
  - `NumLevels`：金字塔层数
  - `Greediness`：贪婪度
  - `Row`：匹配的位置行坐标
  - `Column`：匹配的位置列坐标
  - `Angle`：匹配的角度
  - `Score`：匹配的分数
```

### 二、缺陷检测

#### 1. Blob 分析

- `threshold`：阈值分割图像

```yaml
- `threshold (Image : input, MinGray : input, MaxGray : input, Region : output)`
  - `Image`：输入图像
  - `MinGray`：最低灰度值
  - `MaxGray`：最高灰度值
  - `Region`：输出的二值区域
```

- `connection`：连接组件

```yaml
- `connection (Region : input, ConnectedRegions : output)`
  - `Region`：输入的二值区域
  - `ConnectedRegions`：输出的连接区域
```

- `select_shape`：选择符合形状条件的组件

```yaml
- `select_shape (Regions : input, SelectedRegions : output, Features : input, Operation : input, Min : input, Max : input)`
  - `Regions`：输入的连接区域
  - `SelectedRegions`：输出的选择区域
  - `Features`：形状特征，如“area”
  - `Operation`：比较操作，如“and”
  - `Min`：最小值
  - `Max`：最大值
```

- `area_center`：计算区域的面积和质心

```yaml
- `area_center (Region : input, Area : output, Row : output, Column : output)`
  - `Region`：输入的区域
  - `Area`：区域的面积
  - `Row`：区域的质心行坐标
  - `Column`：区域的质心列坐标
```

#### 2. 缺料判断（通过面积判断）

- `threshold`：阈值分割图像

```yaml
参数同上
```

- `connection`：连接组件

```yaml
：参数同上
```

- `select_shape`：选择符合形状条件的组件

```yaml
：参数同上
```

### 三、正反面区分

- `find_shape_model` 或 `find_ncc_model`：匹配图像特征来区分正反面

```yaml
：参数同上
```

- `angle_ll`：计算匹配的角度，判断正反面

```yaml
- `angle_ll (Angle1 : input, Angle2 : input, MinDifference : output)`
  - `Angle1`：第一个角度
  - `Angle2`：第二个角度
  - `MinDifference`：输出的最小角度差
```

### 四、通讯

#### 1. TCP 通讯

- `open_socket`：打开 TCP 连接

```yaml
- `open_socket (Socket : output, HostName : input, Port : input)`
  - `Socket`：输出的套接字句柄
  - `HostName`：主机名
  - `Port`：端口号
```

- `send_data`：发送数据

```yaml
- `send_data (Socket : input, Data : input)`
  - `Socket`：套接字句柄
  - `Data`：要发送的数据
```

- `receive_data`：接收数据

```yaml
- `receive_data (Socket : input, MaxLength : input, Data : output)`
  - `Socket`：套接字句柄
  - `MaxLength`：最大接收数据长度
  - `Data`：接收到的数据
```

- `close_socket`：关闭 TCP 连接

```yaml
- `close_socket (Socket : input)`
  - `Socket`：套接字句柄
```

#### 2. Modbus 通讯

- `open_modbus`：打开 Modbus 连接

- `send_data`：发送数据
 
- `receive_data`：接收数据

- `close_modbus`：关闭 Modbus 连接


### 五、视觉标定

#### 1. 九点标定

- `calibrate_hand_eye`：手眼标定

```yaml
- `calibrate_hand_eye (CalibDataID : input, CalibSetup : input, CalibObject : input, BaseData : input, HandEyeSetup : input, CalibDataIDOut : output)`
  - `CalibDataID`：标定数据ID
  - `CalibSetup`：标定设置
  - `CalibObject`：标定物体
  - `BaseData`：基础数据
  - `HandEyeSetup`：手眼设置
  - `CalibDataIDOut`：输出的标定数据ID
```

- `find_calib_object`：找到标定物

```yaml
- `find_calib_object (Image : input, CalibDataID : input, CalibObjectIdx : input, Pose : output)`
  - `Image`：输入图像
  - `CalibDataID`：标定数据ID
  - `CalibObjectIdx`：标定物体索引
  - `Pose`：输出的位姿
```

- `calibrate_cameras`：相机标定

```yaml
- `calibrate_cameras (CalibDataID : input, CameraParameters : output, FinalError : output)`
  - `CalibDataID`：标定数据ID
  - `CameraParameters`：输出的相机参数
  - `FinalError`：最终误差
```

#### 2、矩阵变换

```c# title="生成矩阵"
HTuple hv_HomMat2Dx;
HOperatorSet.HomMat2dIdentity(out hv_HomMat2Dx);
HOperatorSet.VectorToHomMat2d(hRows, hCols, hXs, hYs, out hv_HomMat2Dx);


```

```c# title="通过矩阵换算坐标"
public static bool Fun_cam2XY(Job job, Calibration info, DCoord hCoord, out DCoord Coord)
{
    Coord = new DCoord();
    try
    {
        double x = hCoord.X * info.HomMat[0] + hCoord.Y * info.HomMat[1] + info.HomMat[2];
        double y = hCoord.X * info.HomMat[3] + hCoord.Y * info.HomMat[4] + info.HomMat[5];

        double theta_off = Math.Atan2(info.Offset_y, info.Offset_x);  //补偿在产品坐标系的夹角
        double delta_R = Math.Sqrt(Math.Pow(info.Offset_x, 2) + Math.Pow(info.Offset_y, 2));

        x += Math.Cos(hCoord.angle.ToAngle() + theta_off) * delta_R;
        y += Math.Sin(hCoord.angle.ToAngle() + theta_off) * delta_R;
        double theta = hCoord.angle + info.Offset_theta.ToAngle();

        Coord = new DCoord(x, y, theta);
    }
    catch (Exception ex)
    {
        job.form_Infor.OutputMsg("像素坐标转换到世界坐标错误\n" + ex.ToString(), Color.Red);
        return false;
    }
    return true;
}
```

```C# title="HalconExtension.cs"
public static class HalconExtension
{
    /// <summary>
    /// 获取反射变换矩阵
    /// </summary>
    /// <param name="hv_HomMat2D"></param>
    /// <param name="Follow"></param>
    /// <param name="matching"></param>
    /// <returns></returns>
    public static void VectorAngleToRigid(DCoord Follow, DCoord matching,out HTuple hv_HomMat2D)
    {
        HOperatorSet.VectorAngleToRigid(Follow.Y, Follow.X, Follow.angle.ToRadians(),
                                        matching.Y, matching.X, matching.angle.ToRadians(),
                                        out hv_HomMat2D);
    }

    /// <summary>
    /// 获取反射变换区域
    /// </summary>
    /// <param name="Follow"></param>
    /// <param name="matching"></param>
    /// <param name="hObject"></param>
    /// <param name="regionGet"></param>
    public static void GetTransRegion(DCoord Follow, DCoord matching, HObject hObject, out HObject regionGet)
    {
        VectorAngleToRigid(Follow, matching, out HTuple hv_HomMat2D);
        HOperatorSet.AffineTransRegion(hObject, out regionGet, hv_HomMat2D, "nearest_neighbor");
    }

    /// <summary>
    /// 获取反射变换轮廓
    /// </summary>
    /// <param name="Follow"></param>
    /// <param name="matching"></param>
    /// <param name="contours"></param>
    /// <param name="contoursAffineTrans"></param>
    public static void GetTransContourXld(DCoord Follow, DCoord matching, HObject contours, out HObject contoursAffineTrans)
    {
        VectorAngleToRigid(Follow, matching, out HTuple hv_HomMat2D);
        HOperatorSet.AffineTransContourXld(contours, out contoursAffineTrans, hv_HomMat2D);
    }

    /// <summary>
    /// 获取反射变换点
    /// </summary>
    /// <param name="Follow"></param>
    /// <param name="matching"></param>
    /// <param name="row"></param>
    /// <param name="col"></param>
    /// <param name="rowTrans"></param>
    /// <param name="colTrans"></param>
    public static void GetTransPixel(DCoord Follow, DCoord matching, HTuple row, HTuple col, out HTuple rowTrans, out HTuple colTrans)
    {
        VectorAngleToRigid(Follow, matching, out HTuple hv_HomMat2D);
        HOperatorSet.AffineTransPixel(hv_HomMat2D, row, col,out rowTrans, out colTrans);
    }

    /// <summary>
    /// 获取反射变换区域和点
    /// </summary>
    /// <param name="Follow"></param>
    /// <param name="matching"></param>
    /// <param name="hObject"></param>
    /// <param name="regionGet"></param>
    /// <param name="row"></param>
    /// <param name="col"></param>
    /// <param name="rowTrans"></param>
    /// <param name="colTrans"></param>
    public static void GetTransRegionAndPixel(DCoord Follow, DCoord matching, HObject hObject, out HObject regionGet, HTuple row, HTuple col, out HTuple rowTrans, out HTuple colTrans)
    {
        VectorAngleToRigid(Follow, matching, out HTuple hv_HomMat2D);
        HOperatorSet.AffineTransRegion(hObject, out regionGet, hv_HomMat2D, "nearest_neighbor");
        HOperatorSet.AffineTransPixel(hv_HomMat2D, row, col, out rowTrans, out colTrans);
    }

}
```

### 六、工具坐标系

- `create_pose`：创建位姿

```yaml
- `create_pose (TransX : input, TransY : input, TransZ : input, RotX : input, RotY : input, RotZ : input, Order : input, Pose : output)`
  - `TransX`：X 轴平移
  - `TransY`：Y 轴平移
  - `TransZ`：Z 轴平移
  - `RotX`：X 轴旋转
  - `RotY`：Y 轴旋转
  - `RotZ`：Z 轴旋转
  - `Order`：旋转顺序
  - `Pose`：输出的位姿
```

- `set_origin_pose`：设置原点位姿

```yaml
- `set_origin_pose (PoseIn : input, PoseOut : output)`
  - `PoseIn`：输入位姿
  - `PoseOut`：输出设置为原点的位姿
```

- `compose_pose`：合成位姿

```yaml
- `compose_pose (Pose1 : input, Pose2 : input, PoseOut : output)`
  - `Pose1`：第一个位姿
  - `Pose2`：第二个位姿
  - `PoseOut`：输出合成的位姿
```

### 七、坐标系要求

- 发送给机械臂控制器的坐标应该是基于机械臂坐标系下的：

- `pose_trans`：转换位姿
    
```yaml
- `pose_trans (PoseIn : input, TransX : input, TransY : input, TransZ : input, PoseOut : output)`
    - `PoseIn`：输入位姿
    - `TransX`：X 轴平移
    - `TransY`：Y 轴平移
    - `TransZ`：Z 轴平移
    - `PoseOut`：输出的位姿
```

- `vector_to_pose`：将坐标转换为位姿

```yaml
- `vector_to_pose (Vector : input, Pose : output)`
- `Vector`：输入的向量
- `Pose`：输出的位姿
```