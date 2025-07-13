# Your Approach and Methodology

I use a YOLO-based object detector 'YOLOv11' via Ultralytics (best.pt) to detect football players frame-by-frame in given video (15sec_input_720p.mp4). Detected bounding boxes are passed to the Deep SORT tracker, which assigns consistent player IDs across frames using appearance features and motion estimation. Boxes showing player positions and their ID numbers are drawn on the video frames, and the updated video is saved as a new file (output.mp4).


# Techniques Tried and Their Outcomes

### Color Histogram Embeddings:

The first technique involved using color histograms to capture the visual appearance of players. However, this method proved ineffective in maintaining consistent identities. Since many players wore similar jerseys, and because of changing lighting and players blocking each other, the color information wasn’t reliable. This made it hard to tell players apart, resulting in poor tracking performance.

### YOLO Detection:

- Players are filtered based on confidence score (conf > 0.6) and size (width/height > 10).
- Only class "player" is retained from YOLO detections.

### Deep SORT Tracking:

- Used mobilenet as an appearance embedder.
- Tracker settings tuned for ID stability:
  - max_age=200, n_init=5, max_cosine_distance=0.2, etc.
- Tracks are updated per frame and visualized in real-time.


# Challenges Encountered:

### - ID Switches: 
  Due to occlusions or similar appearances, player IDs sometimes changed between frames.

### - Bounding Box Noise:
  Small or partially visible players were filtered out to improve tracking consistency.

### - Speed:
  Real-time display with matplotlib is slow; consider using OpenCV's imshow() for real-time visualization.

### - Choosing best embedder:
  TorchreID can be a good option for improving accuracy and maintaining consistent player IDs, as it offers a variety of powerful      
  re-identification models.However, it has some drawbacks: runtime errors due to complex and heavy dependencies, training and inference are slow, especially on limited hardware.
  For this reason, I preferred using a lightweight embedder like **MobileNet**, which provided a better balance of speed, maintaining acceptable re-identification accuracy and performance in my setup.

### - Filtering Detections and Parameter Tuning:
  I filtered out low-confidence detections and very small boxes to avoid noisy tracking.  
  I also fine-tuned Deep SORT parameters like `max_age`, `n_init`, `nms_max_overlap`, `max_iou_distance`, `max_cosine_distance`, and `nn_budget`. These adjustments had a major effect on tracking stability and identity preservation.


# Future Improvements:

Even after trying my best and many methods to improve player re-identification, the results were limited. Usually, only some players were correctly identified again after leaving and coming back into the frame. The rest were given new IDs. I tried several things, like removing low-confidence or tiny detections, adjusting Deep SORT settings (like max_age, n_init, and max_cosine_distance), and using MobileNet for faster and efficient appearance matching. I also tested other re-ID models from TorchreID, but keeping player IDs consistent was still difficult—especially when players looked similar, moved fast, or got blocked from view.

### With additional time and resources, I would try to:
  **Build a custom re-ID model** trained on football match videos to better understand how players look and improve identification accuracy.
  **Make tracking more consistent over time** by using player movement paths to help recognize them when they come back into view.
  **Use extra information** like jersey numbers or team colors, to fix mistakes in player identity.
  **Try memory-based tracking**, which remembers how players looked over a longer time to help re-identify them later.
  **Explore TorchreID in more depth**, including its model options and dependency setup, to better understand its potential for improving ID consistency in tracking tasks.


