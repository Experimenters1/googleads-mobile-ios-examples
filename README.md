# googleads-mobile-ios-examples
#
## googleads-mobile-ios-examples
#
[Get Started](https://developers.google.com/admob/ios/quick-start) <br><br>

[Google Mobile Ads SDK for iOS](https://github.com/googleads/googleads-mobile-ios-examples) <br><br>


#
## Banner Ads

[**Banner Ads**](https://developers.google.com/admob/ios/banner) <br><br>

#
```swift
import GoogleMobileAds

class Video_Source: UIViewController,GADBannerViewDelegate   {
         var bannerView: GADBannerView!
         

      override func viewDidLoad() {
        super.viewDidLoad()
        
               let adSize = GADAdSizeFromCGSize(CGSize(width: view.frame.width, height: 55))
        bannerView = GADBannerView(adSize: adSize)
        bannerView.delegate = self
        addBannerViewToView(bannerView)
        bannerView.adUnitID = "ca-app-pub-3940256099942544/2934735716"
        bannerView.backgroundColor = UIColor.clear

        bannerView.layer.borderWidth = 2.0
        bannerView.layer.borderColor = UIColor.clear.cgColor
        bannerView.rootViewController = self
        bannerView.load(GADRequest())
      }

 func addBannerViewToView(_ bannerView: GADBannerView) {
        bannerView.translatesAutoresizingMaskIntoConstraints = false
        view.addSubview(bannerView)
        view.addConstraints(
          [NSLayoutConstraint(item: bannerView,
                              attribute: .bottom,
                              relatedBy: .equal,
                              toItem: view.safeAreaLayoutGuide,
                              attribute: .bottom,
                              multiplier: 1,
                              constant: 0),
           NSLayoutConstraint(item: bannerView,
                              attribute: .centerX,
                              relatedBy: .equal,
                              toItem: view,
                              attribute: .centerX,
                              multiplier: 1,
                              constant: 0)
          ])
       }
    
    
    func bannerViewDidReceiveAd(_ bannerView: GADBannerView) {
      print("bannerViewDidReceiveAd")
    }

    func bannerView(_ bannerView: GADBannerView, didFailToReceiveAdWithError error: Error) {
      print("bannerView:didFailToReceiveAdWithError: \(error.localizedDescription)")
    }

    func bannerViewDidRecordImpression(_ bannerView: GADBannerView) {
      print("bannerViewDidRecordImpression")
    }

    func bannerViewWillPresentScreen(_ bannerView: GADBannerView) {
      print("bannerViewWillPresentScreen")
    }

    func bannerViewWillDismissScreen(_ bannerView: GADBannerView) {
      print("bannerViewWillDIsmissScreen")
    }

    func bannerViewDidDismissScreen(_ bannerView: GADBannerView) {
      print("bannerViewDidDismissScreen")
    }
    


}

```
#

## Interstitial ads

[**Interstitial ads**](https://developers.google.com/admob/ios/interstitial) <br><br>

#

```swift
import GoogleMobileAds

class ViewController: UIViewController, GADFullScreenContentDelegate {

    private var interstitial: GADInterstitialAd?

    override func viewDidLoad() {
        super.viewDidLoad()
        loadAd()
    }

    func loadAd() {
        let request = GADRequest()
        GADInterstitialAd.load(
            withAdUnitID: "ca-app-pub-3940256099942544/4411468910",
            request: request,
            completionHandler: { [self] ad, error in
                if let error = error {
                    print("Failed to load interstitial ad with error: \(error.localizedDescription)")
                    return
                }
                interstitial = ad
                interstitial?.fullScreenContentDelegate = self
            }
        )
    }

    func showAd() {
        if let interstitial = interstitial {
            let root = UIApplication.shared.keyWindow!.rootViewController
            interstitial.present(fromRootViewController: root!)
        } else {
            // Quảng cáo chưa sẵn sàng, bạn có thể xử lý ở đây hoặc bỏ qua.
            // Ví dụ: Hiển thị màn hình tiếp theo trực tiếp.
            self.presentNextViewController()
        }
    }

    // Được gọi khi quảng cáo đã hoàn thành
    func adDidDismissFullScreenContent(_ ad: GADFullScreenPresentingAd) {
        print("Ad did dismiss full screen content.")
        loadAd() // Tải quảng cáo mới để chuẩn bị cho lần sau
        showAd() // Hiển thị quảng cáo hoặc chuyển sang màn hình tiếp theo
    }

    // Được gọi khi quảng cáo không thể hiển thị
    func ad(_ ad: GADFullScreenPresentingAd, didFailToPresentFullScreenContentWithError error: Error) {
        print("Ad did fail to present full screen content.")
        self.presentNextViewController() // Chuyển sang màn hình tiếp theo nếu quảng cáo không thể hiển thị
    }

    // Hàm để chuyển sang màn hình tiếp theo
    func presentNextViewController() {
        let nextViewController = UIViewController() // Thay bằng màn hình tiếp theo của bạn
        self.navigationController?.pushViewController(nextViewController, animated: true)
    }
}

```
