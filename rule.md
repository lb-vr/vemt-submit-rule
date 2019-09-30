# A. 環境構築

1. Unityのバージョンは2017.4.28f1を使用すること。
1. VRCSDKは公式から配布される最新バージョンで運用されること。
1. 以下のルールにおいての基本的な構造を作成するため、environment.unitypackageをインポートすること。
1. Assetsフォルダルートにフォルダを作成し、ブースのアセットはその中にすべて入れること。
1. 作成したフォルダにシーンを作成し、そのシーンにおいてブースを作成すること。

なお、environment.unitypackageをインポートすることで、ルールA4・A5に基づき、自動的にフォルダとシーンがAssets内に作成されます。

# B. ファイル・フォルダ名規定
1. メッシュ名、マテリアル名、シェーダー名など含む、すべてのアセット・フォルダ名は、半角英数、「-」（ハイフン）、「_」（アンダーバー）、「 」（スペース）、「.」（ドット）、「（）」（丸カッコ）のみ使用可能。
1. 全てのファイルにおいて、Assetsフォルダからの相対パスは、100文字以内に収まること。
1. 「.blend」ファイルなど、Unityが標準で対応しないアセットは一切使用できない。

# C. Scene内階層形式規定
1. シーン内に「booth」という名前のEmptyオブジェクトを作成し、座標は原点とすること。大文字小文字は問わない。全てのブースオブジェクトは、この「Booth」オブジェクト内にあること。
1. シーンヒエラルキーのルートに、「booth」と同名のオブジェクトを置かないこと。大文字小文字違いも不可。
1. 「booth」オブジェクト以下のオブジェクトに対する、Static設定は適切に行うこと。

なお、environment.unitypackageをインポートすることで、ルールC1・C2に基づき、自動的にフォルダとシーンがAssets内に作成されます。

# D. ブース規定
1. ブースの寸法は、幅4m以内、奥行4m以内、高さ5m以内で作成すること。
1. Z+方向をブースの正面とすること。
1. X軸方向に対しては、ブースの中央を原点とすること。
1. Y軸方向に対しては、ブースの底面を原点とすること。
1. Z軸方向に対しては、ブースの最手前面を原点とすること。
1. 使用するマテリアル数は10個以内を目指し、必ず12個以内に収めること。ただし、UnityのBuilt-inマテリアルは含まない
1. テクスチャの枚数制限はないが、ただしアトラス化(統合)、およびクランチ圧縮を強く推奨。
1. Lightmap Staticが設定されたオブジェクトは、20個以内に収めること。またLightmapのスケール値は1であること。(** TODO:スケール値は1？ **)
1. ブースデータとVRC_Worldを置いた状態での、ワールドアップロード時のサイズが11MB未満であること。
1. Directional LightやCameraなどを除いた、ブースデータのみの状態で実行し、Batchesは30以内を目指し、35以内に収めること。
1. Directional LightやCameraなどを除いた、ブースデータのみの状態で実行し、SetPassCallsは20以内を目指し、25以内に収めること。

なお、合同ブース対応はありません。

# E. シェーダー規定

1. 運営は、共通で使用される外部シェーダーと、そのバージョンを指定すること。
1. 出展者は、指定されたシェーダーとバージョンを利用する場合は、シェーダーファイルを含めずに入稿すること。
1. また、指定されていないシェーダー、バージョン違いのシェーダーを使用する場合は、シェーダーファイルを含めて入稿すること。cgincファイルなども全て含めること。
1. 自作シェーダーはキーワード数を低く抑えること。
1. _CameraDepthTextureは使用できない。

# F. Component規定

## F-1. 使用可能なComponent

### VRCSDK関連
1. VRC_Trigger
    1. Advanced Modeを有効化。
    1. Broadcast TypeはLocalのみ。
    1. Triggerモードは以下のうちいずれか。
        1. Custom
        1. OnInteract
        1. OnEnterTrigger
        1. OnExitTrigger
        1. OnPickup
        1. OnDrop
        1. OnPickupUseDown
        1. OnPickupUseUp
1. Action
    1. Animation*
    1. ActivateCustomTrigger
    1. AudioTrigger
    1. PlayAnimation
    1. SetComponentActive
    1. SetGameObjectActive
    1. SetParticlePlaying
    1. SetAvatarUseに対するSendRPC
        1. targetはLocalのみ。
1. VRC_Object Sync
    1. booth_template.unitypackageに含まれるPickupObjectSyncでのみ使用可能。
    1. オブジェクトを非アクティブにしてはならない。
    1. Allow Collision Transferは無効化すること。
1. VRC_Pickup
    1. booth_template.unitypackageに含まれるPickupObjectSync、またはPickupObjectでのみ使用可能。
    1. 最大5つまで使用可能。
1. VRC_Station
    1. TODO
1. VRC_Tutorial Area Marker
1. VRC_Audio Bank
1. VRC_Avatar Pedestal
1. VRC_Ui Shape
### 物理演算関連
1. Rigidbody
    配布Prefab以外での使用は応相談
1. Cloth
    できるだけ負荷軽減に努めること。
1. Collider
    1. 使用可能なコライダの種類
        1. Box Collider
        1. Sphere Collider
        1. Cupsule Collider
    1. ブース範囲内に収まること。
    1. Mesh Colliderは使用できない。
1. Dynamic Bone
    1. Dynamic Boneが影響するボーン数は64以内に収めること。
    1. ペデスタルアバターのDynamic Boneは、VRChat公式のペデスタルアバター規定を守ること。
1. Dynamic Bone Collider
    1. Dynamic Bone Colliderの数は8以内に収めること。
    1. ペデスタルアバターのDynamic Boneは、VRChat公式のペデスタルアバター規定を守ること。
### Rendering / Effect関連
1. Skinned Mesh Renderer
    1. Boundsがブース範囲内に収まること。
1. Mesh Renderer / Mesh Filter
1. Particle System
    1. Max Particleは1000以内に収めること。
    1. CollisionはPlaneのみ使用可能。
1. Trail Renderer / Line Renderer
### Light
1. Bakedのみ使用可能。
1. ライトの影響範囲（Range）が、ブースから極力はみ出さないようにすること。
1. Light Probe Group
    1. 最大64個以内に収めること。
1. Reflection Probe
    1. Custom Reflection Probe
        1. 数の制限・解像度の制限はない。
        1. ベイク済みテクスチャは入稿ファイルに含め、またワールドアップロード時の容量カウントに含まれる。
    1. Baked Reflection
        1. 最大2個以内に収めること。
        1. 解像度は256以内にすること。
### その他
1. Animator / Animation
Boneを動かすものは負荷が高めなので注意
VRC_PickupおよびVRC_ObjectSyncとAnimatorの併用は不可
「../」の使用不可
Material変更の禁止
Culling Modeは動作上問題がなければCull Completly推奨
Audio Source
音の鳴る範囲を制限された配布Prefabを使用すること
Loopで使う場合は限界突破ブースを申請し初期状態では鳴らないようにすること
Canvas関連
看板等の表示としての使用を強く推奨
Vケットから配布するPrefabの利用推奨

## F-2. 使用禁止なComponent
基本は使用可能なComponentに記述されていないComponentである。

1. VRC_Mirror

# Z. ペデスタルアバター規定
VRC_Avatar Pedestalに設定するアバターは以下を守ること。
1. ポリゴン数 70000以下
1. Skinned Mesh Renderer 8以下
1. Material Slot 16以下
1. Dynamic Boneが影響するTransform数 32以下
1. Dynamic Bone Collider 2以下

> 参照：VRChat World Submission and Optimization Guidelines

