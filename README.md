- 👋 Hi, I’m @ama324
- 👀 I’m interested in ...
- 🌱 I’m currently learning ...
- 💞️ I’m looking to collaborate on ...
- 📫 How to reach me ...

<!---
ama324/ama324 is a ✨ special ✨ repository because its `README.md` (this file) appears on your GitHub profile.
You can click the Preview link to take a look at your changes.
--->
package com.example.wallpaperapp;

import android.content.Context;
import android.content.Intent;
import android.net.Uri;
import android.os.Bundle;
import android.view.View;
import android.widget.Button;
import android.widget.ImageView;
import android.widget.TextView;

public class WallpaperActivity extends AppCompatActivity {

    private ImageView wallpaperImage;
    private TextView wallpaperTitle;
    private Button setWallpaperButton;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_wallpaper);

        wallpaperImage = findViewById(R.id.wallpaper_image);
        wallpaperTitle = findViewById(R.id.wallpaper_title);
        setWallpaperButton = findViewById(R.id.set_wallpaper_button);

        // Get the wallpaper data from the intent
        Intent intent = getIntent();
        String wallpaperUrl = intent.getStringExtra("wallpaper_url");
        String wallpaperTitleText = intent.getStringExtra("wallpaper_title");

        // Set the wallpaper image and title
        wallpaperImage.setImageURI(Uri.parse(wallpaperUrl));
        wallpaperTitle.setText(wallpaperTitleText);

        // Set the wallpaper button click listener
        setWallpaperButton.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                // Set the wallpaper
                setWallpaper(wallpaperUrl);
            }
        });
    }

    // Set the wallpaper
    private void setWallpaper(String wallpaperUrl) {
        // Get the wallpaper manager
        Context context = getApplicationContext();
        WallpaperManager wallpaperManager = WallpaperManager.getInstance(context);

        // Set the wallpaper
        try {
            wallpaperManager.setWallpaper(Uri.parse(wallpaperUrl));
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
