package albumproject;

public class Album implements IAlbum {

    // Inner Node class
    class Node {
        Photo data;
        Node prev;
        Node next;

        Node(Photo data) {
            this.data = data;
        }
    }

    // Fields
    private String albumName;
    private int count = 0;
    private Node current = null;
    private boolean isOpen = false;

    // Constructor
    public Album(String albumName) {
        this.albumName = albumName;
    }

    // Methods

    @Override
    public String getAlbumName() {
        return albumName;
    }

    @Override
    public int getCount() {
        return count;
    }

    @Override
    public void openAlbum() {
        if (!isOpen) {
            isOpen = true;
            System.out.println("Album " + albumName + " opened.");
            if (current != null) {
                current.data.viewPhoto();
            }
        }
    }

    @Override
    public void closeAlbum() {
        if (isOpen) {
            isOpen = false;
            System.out.println("Album " + albumName + " closed.");
        }
    }

    @Override
    public boolean hasPhoto(Photo photo) {
        if (current == null) {
            return false;
        }
        Node temp = current;
        do {
            if (temp.data.equals(photo)) {
                return true;
            }
            temp = temp.next;
        } while (temp != current);
        return false;
    }

    @Override
    public void addPhoto(Photo photo) {
        if (hasPhoto(photo)) {
            System.out.println("Attempted to add duplicate photo.");
            return;
        }
        Node newNode = new Node(photo);
        if (current == null) {
            // First photo added
            current = newNode;
            current.next = current;
            current.prev = current;
        } else {
            // Insert newNode before current
            Node last = current.prev;
            newNode.next = current;
            newNode.prev = last;
            last.next = newNode;
            current.prev = newNode;
            // Do NOT update current
        }
        count++;
    }

    @Override
    public void deletePhoto(Photo photo) {
        if (current == null) {
            System.out.println("Attempted to delete a photo that is not in the album.");
            return;
        }
        Node temp = current;
        boolean found = false;
        do {
            if (temp.data.equals(photo)) {
                found = true;
                break;
            }
            temp = temp.next;
        } while (temp != current);

        if (!found) {
            System.out.println("Attempted to delete a photo that is not in the album.");
            return;
        }

        if (temp.next == temp) {
            // Only one node in the list
            current = null;
        } else {
            temp.prev.next = temp.next;
            temp.next.prev = temp.prev;
            if (current == temp) {
                current = temp.next;
            }
        }
        count--;
    }

    @Override
    public boolean allPhotosViewed() {
        if (current == null) {
            return true;
        }
        Node temp = current;
        do {
            if (!temp.data.isViewed()) {
                return false;
            }
            temp = temp.next;
        } while (temp != current);
        return true;
    }

    @Override
    public void viewNextPhoto() {
        if (!isOpen) {
            System.out.println("Tried to view next photo, but album is closed.");
            return;
        }
        if (current == null) {
            System.out.println("Tried to view next photo, but album has no photos.");
            return;
        }
        current = current.next;
        current.data.viewPhoto();
    }

    @Override
    public void viewPreviousPhoto() {
        if (!isOpen) {
            System.out.println("Tried to view previous photo, but album is closed.");
            return;
        }
        if (current == null) {
            System.out.println("Tried to view previous photo, but album has no photos.");
            return;
        }
        current = current.prev;
        current.data.viewPhoto();
    }

    @Override
    public boolean equals(IAlbum other) {
        if (other == null || this.getCount() != other.getCount()) {
            return false;
        }
        java.util.HashSet<Photo> thisPhotos = new java.util.HashSet<>();
        if (current != null) {
            Node temp = current;
            do {
                thisPhotos.add(temp.data);
                temp = temp.next;
            } while (temp != current);
        }
        // Assuming other is also an instance of Album
        Album otherAlbum = (Album) other;
        java.util.HashSet<Photo> otherPhotos = new java.util.HashSet<>();
        if (otherAlbum.current != null) {
            Node temp = otherAlbum.current;
            do {
                otherPhotos.add(temp.data);
                temp = temp.next;
            } while (temp != otherAlbum.current);
        }
        return thisPhotos.equals(otherPhotos);
    }

    // Additional method to check if album is empty
    public boolean isEmpty() {
        return count == 0;
    }

    
    public static void main(String[] args) {
    	System.out.println("/|\\ /|\\ /|\\ /|\\ /|\\ /|\\");
    	System.out.println("\nSample output 6\n");
    	System.out.println("Testing edge cases");
    	Album album = new Album("My Cool Album");
    	Photo photo1 = new Photo("Sunset", "abc123");
    	Photo photo2 = new Photo("Sunrise", "def456");
    	Photo photo3 = new Photo("Can of Beans", "ghi789");
    	album.addPhoto(photo1);
    	album.addPhoto(photo2);
    	album.addPhoto(photo3);
    	System.out.println("\nDeleting current photo should make next photo current:");
    	album.openAlbum();
    	album.viewNextPhoto();
    	album.closeAlbum();
    	album.deletePhoto(photo2);
    	album.openAlbum();
    	album.closeAlbum();
    	album.deletePhoto(photo3);
    	album.openAlbum();
    	album.closeAlbum();
    	System.out.println("\nAlbum with no photos should be considered viewed:");
    	album.deletePhoto(photo1);
    	System.out.println("Is album empty? " + album.isEmpty());
    	System.out.println("Are all photos in album viewed? " + album.allPhotosViewed());
    	System.out.println("\nAlbum that is viewed should become unviewed once new photo is added:");
    	album.addPhoto(new Photo("Shredding the Gnar", "012345"));
    	album.openAlbum();
    	System.out.println("Are all photos in album viewed? " + album.allPhotosViewed());
    	album.addPhoto(new Photo("Hanging Ten", "678901"));
    	System.out.println("Are all photos in album viewed? " + album.allPhotosViewed());
    	System.out.println("\n\\|/ \\|/ \\|/ \\|/ \\|/ \\|/");


    }
    
    
}
