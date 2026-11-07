# Image specs (canonical)

The accepted image shapes per platform. Each feed crops or downscales anything off-spec,
so an image outside these ratios gets mangled.

**Nothing in this project renders an image.** Since 2026-10-08 the only images are the
owner's own screenshots and photos, filed by `post-image`. An artifact keeps its own
shape as long as it sits inside the range below; a screenshot forced square is a cropped
screenshot, so crop to the region that matters, not to a ratio.

## LinkedIn feed image

| shape | pixels (reference) | ratio | notes |
| --- | --- | --- | --- |
| `landscape` | 1200 x 627 | 1.91:1 | the widest LinkedIn shows without cropping |
| `square` | 1200 x 1200 | 1:1 | fine for a cropped dashboard or table |
| `portrait` | 1080 x 1350 | 4:5 | the tallest; most mobile feed space |

Anything between 1.91:1 and 4:5 displays as is. Up to four images per post; the first is
the thumbnail.

## X feed image

| shape | pixels (reference) | ratio | notes |
| --- | --- | --- | --- |
| `landscape` | 1600 x 900 | 16:9 | the widest X shows uncropped |
| `square` | 1200 x 1200 | 1:1 | |
| `portrait` | 1080 x 1350 | 4:5 | taller images are cropped in the timeline |

Anything between 16:9 and 4:5 displays as is. Up to four images per post; the first is
the preview.

## File rules

- PNG or JPEG. Keep each file under 5 MB.
- No overlay text, frames, or compositing; the real screen as it was.

## Sources

- https://www.sendible.com/insights/linkedin-post-size
- https://www.linkedin.com/help/linkedin/answer/a563309/image-specifications-for-your-linkedin-pages-and-career-pages
- https://help.x.com/en/using-x/x-images
